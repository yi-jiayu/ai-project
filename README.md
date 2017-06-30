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
5. Wait for training to complete. The test set accuracy will the shown.
6. You can find the generated graph and labels at `/tmp/output_graph.pb` and `/tmp/output_labels.txt`.
7. Run `label_image.py` with the `--graph`, `--labels` and `--image` flags to get a prediction for a specified image.
