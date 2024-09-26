# Wildfire VIP
Fire prediction and simulation for VIP with Prof. Bo Zhu and mentor Duowen.

# Unity Sim
Data generated using [GPU-GEMS-3D-Fluid-Simulation](https://github.com/Scrawk/GPU-GEMS-3D-Fluid-Simulation) GPU based simulation in Unity. We use a simple CNN with L2 regularization to predict the Temperature Amount parameter from image, based on the flame shape, smoke amount, and color.

## Results
The Mean Absolute Error of the model's predictions on the test dataset is 10.53 after 150 epochs (LR=0.0001, batch_size=16).
We take two different images of the fire per each "Temperature Amount", which ranges from 5 to 200. So, we have 390 synthetic images. We use 80% as training data and 20% as test data.

Below are some example temperature predictions on 3 images. Images can be found in the `unitySim/UnitySim5-200` folder.
```
Image: Temp1_022.png
Predicted temperature: 32.17
Actual temperature: 22.00
Absolute error: 10.17

Image: Temp1_102.png
Predicted temperature: 107.19
Actual temperature: 102.00
Absolute error: 5.19

Image: Temp_197.png
Predicted temperature: 175.44
Actual temperature: 197.00
Absolute error: 21.56
```

Below is a graph of the MAE per each image in the test set, with the X axis being test set images. Images are ordered from lowest temperature (01) to highest temperature().


# Embergen Generic Fire
Synthetic data generated in Embergen of a thin candle flame. We use a CNN to predict temperature from image, due to flame shape and color.
## Results
The Mean Absolute Error of the model's predictions on the test dataset is 39.92 after 50 epochs.

Below are some example temperature predictions on 3 images. Images can be found in the `genericFire/GenericFire3000-5000K` folder.

```
Image: generic_fire16_3089.1K.png
Predicted temperature: 3076.68K
Actual temperature: 3089.10K
Absolute error: 12.42K

Image: generic_fire301_4676.9K.png
Predicted temperature: 4734.52K
Actual temperature: 4676.90K
Absolute error: 57.62K

Image: generic_fire346_4927.6K.png
Predicted temperature: 4821.37K
Actual temperature: 4927.60K
Absolute error: 106.23K
```


## Training
In the folder `genericFire`, run `python3 genericFire_train.py`.

This script splits the images in `GenericFire3000-5000K` folder into a training set and a test set. It will use the training set to train a model, which is saved as `genericFire_temperature_model.h5`. The script also generates a text file `genericFire_test_set_filenames.txt` that lists the images in the test set for our reference.

## Inference
In the folder `genericFire`, run `python3 genericFire_inf.py`.

This script runs inference on a list of images from `GenericFire3000-5000K` which were part of the test set. At the bottom of the script, you can modify the `selected_images` list to pick which images you want to run inference on. Make sure they are images in the test set (see `genericFire_test_set_filenames.txt`, generated by `genericFire_train.py`).

You can also uncomment the first few lines in `__main__` to run inference on a *randomly* selected image from the test set.


# Embergen Default Candle
Synthetic data generated in Embergen of a thin candle flame. We use a CNN to predict temperature from image, due to candle shape and color.

## Results
The Mean Absolute Error of the model's predictions on the test dataset is 297.64 after 50 epochs.

Below are some example temperature predictions on 7 images. Images can be found in the `candle/CandleFire3000-10000K` folder.

```
Image: candle3_3087.5K.png
Predicted temperature: 4249.16K
Actual temperature: 3087.50K
Absolute error: 1161.66K

Image: candle46_4341.7K.png
Predicted temperature: 4028.54K
Actual temperature: 4341.70K
Absolute error: 313.16K

Image: candle381_5858.3K.png
Predicted temperature: 5891.45K
Actual temperature: 5858.30K
Absolute error: 33.15K

Image: candle361_6441.7K.png
Predicted temperature: 6589.43K
Actual temperature: 6441.70K
Absolute error: 147.73K

Image: candle338_7112.5K.png
Predicted temperature: 7567.24K
Actual temperature: 7112.50K
Absolute error: 454.74K

Image: candle185_8395.8K.png
Predicted temperature: 8769.85K
Actual temperature: 8395.80K
Absolute error: 374.05K

Image: candle231_9737.5K.png
Predicted temperature: 9553.99K
Actual temperature: 9737.50K
Absolute error: 183.51K
```

## Training
In the folder `candle`, run `python3 candle_train.py`.

This script splits the images in `CandleFire3000-10000K` folder into a training set and a test set. It will use the training set to train a model, which is saved as `candle_temperature_model.h5`. The script also generates a text file `test_set_filenames.txt` that lists the images in the test set for our reference.

## Inference
In the folder `candle`, run `python3 candle_inf.py`.

This script runs inference on a list of images from `CandleFire3000-10000K` which were part of the test set. At the bottom of the script, you can modify the `selected_images` list to pick which images you want to run inference on. Make sure they are images in the test set (see `candle_test_set_filenames.txt`, generated by `candle_train.py`).

You can also uncomment the first few lines in `__main__` to run inference on a *randomly* selected image from the test set.

## Training and Inference Combined
The `candle_combined_train_inf.py` will train and run inference in one script.
