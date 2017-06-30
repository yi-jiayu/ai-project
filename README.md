# ai-project
Project for Summer 2017 50.021 Artificial Intelligence at SUTD

## Dependencies
- Tensorflow
- ImageMagick
- Python
- BreaKHis dataset

## Instructions
1. Run `convert_images_to_jpg.sh` from the `BreaKHis_data\BreaKHis_v1\histology_slides\breast` directory within the BreaKHis dataset to generate jpeg versions of all the images.
2. (optional) Create a backup of the provided splits
3. Run `sed -i 's/png/jpg/g' path/to/split` to change the image paths to use the converted jpeg images.
4. Run `retrain_modified.py`, passing in the `--image_dir`, `--split_dir` and `--zoom_level` flags.
5. Wait for training to complete. You can view the training progress in Tensorboard by running `tensorboard --logdir /tmp/retrain_logs`.
6. The final accuracy on the test set will be shown.
7. You can find the generated graph and labels at `/tmp/output_graph.pb` and `/tmp/output_labels.txt`.
8. Run `label_image.py` with the `--graph`, `--labels` and `--image` flags to get a prediction for a specified image.

## Examples
### Training
```
jiayu@jy-9360:~/ai-project$ python3 retrain_modified.py --image_dir ~/BreaKHis_data/ --split_dir ~/B
reaKHis_data/split1
100 bottleneck files created.
200 bottleneck files created.
300 bottleneck files created.
400 bottleneck files created.
500 bottleneck files created.
...
2017-06-30 22:54:12.744650: Step 3950: Train accuracy = 98.0%
2017-06-30 22:54:12.744880: Step 3950: Cross entropy = 0.098675
2017-06-30 22:54:12.858682: Step 3950: Validation accuracy = 90.0% (N=100)
2017-06-30 22:54:13.816888: Step 3960: Train accuracy = 99.0%
2017-06-30 22:54:13.817124: Step 3960: Cross entropy = 0.098515
2017-06-30 22:54:13.910097: Step 3960: Validation accuracy = 96.0% (N=100)
2017-06-30 22:54:14.844774: Step 3970: Train accuracy = 100.0%
2017-06-30 22:54:14.845007: Step 3970: Cross entropy = 0.082367
2017-06-30 22:54:14.936767: Step 3970: Validation accuracy = 87.0% (N=100)
2017-06-30 22:54:15.887153: Step 3980: Train accuracy = 99.0%
2017-06-30 22:54:15.887507: Step 3980: Cross entropy = 0.097011
2017-06-30 22:54:15.977508: Step 3980: Validation accuracy = 88.0% (N=100)
2017-06-30 22:54:17.030560: Step 3990: Train accuracy = 100.0%
2017-06-30 22:54:17.031125: Step 3990: Cross entropy = 0.106523
2017-06-30 22:54:17.146860: Step 3990: Validation accuracy = 90.0% (N=100)
2017-06-30 22:54:18.005861: Step 3999: Train accuracy = 100.0%
2017-06-30 22:54:18.006084: Step 3999: Cross entropy = 0.084462
2017-06-30 22:54:18.105505: Step 3999: Validation accuracy = 91.0% (N=100)
Final test accuracy = 85.2% (N=745)
Converted 2 variables to const ops.
```


### Prediction output
```
jiayu@jy-9360:~/ai-project$ python3 label_image.py --graph ~/output_graph-split1-40X.pb --labels ~/output_labels.txt --image=~/BreaKHis_data/BreaKHis_v1/histology_slides/breast/malignant/SOB/mucinous_carcinoma/SOB_M_MC_14-13418DE/40X/SOB_M_MC-14-13418DE-40-009.jpg
2017-06-30 22:42:51.937882: W tensorflow/core/framework/op_def_util.cc:332] Op BatchNormWithGlobalNormalization is deprecated. It will cease to work in GraphDef version 9. Use tf.nn.batch_normalization().
malignant (score = 0.99341)
benign (score = 0.00659)
```
