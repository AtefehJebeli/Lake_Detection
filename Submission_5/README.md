"Attention_Res_UNet_Trained_on_Balanced_Data_Robust.ipynb" Notebook

Attention: This submission and submission 4 contains aligned coordinate.

Tiling for Consistency: The original extracted regions in our dataset vary in size. To ensure consistency, we tile these regions into 512x512 patches with overlapping sections and zero padding applied as needed. This part is done in preprocessing Notebook. The tiled folders are available on Google Drive. The resulting tiled images are saved in three separate folders: trained_tiles: Tiled images used for training. mask_tiles: Tiled masks associated with the training data. test_tiles_no_overlap: Tiled test images without overlapping sections.

In this notebook, we train our model using a subset of tiled training images. This subset consists of 4,000 images and their mask. Then, the saved weight is used to initialize the training on the whole training set to save computational resources. The saved model, which is trained on the whole training data set is available on Google Drive under folded "Submission_2_and_1" to directly make a prediction on the 12 test regions.

Making Predictions on Test Images: Once the model is trained, it is then employed to make predictions on all the test images in our dataset.

Code Guidance: In the code cells, you will find a descriptive cell preceding each code cell. These descriptive cells provide valuable information and guidelines for executing each code cell. Note that some cells may require setting specific paths, which are clearly indicated in the code for your convenience.

Note on Sanity Check Cells This notebook contains several sanity check cells that are designed to verify the correctness of the workflow and the accuracy of the predictions. These cells are provided for reference and validation purposes and do not need to be executed during the typical usage of the notebook. Above each sanity check cell, you will find clarifications and explanations regarding its purpose and expected output. Feel free to review these cells to gain insights into the validation steps and to ensure the robustness of your analysis. When running the notebook for its primary purpose, such as training a model, making predictions, or performing post-processing, it is not necessary to execute the sanity check cells unless you have specific debugging or verification needs. In most cases, the primary workflow steps outlined in this README should suffice for your project.

The details of the steps are:

1. Import Libraries and Define Functions and Models: Start by importing the necessary libraries and defining the functions and models required for your task.
Attention: If you download the saved model (best_model_lake_512_512_2k_lake_2k_none_res_attention_fold_1.h5) and test_tiles_no_overlap from Google Drive, You can skip the below step until Part 3.

2. Train the Model: The model is trained using a 2-fold cross-validation approach. The training process involves using a batch size of 12 for 300 epochs. The best model weights are saved to prevent overfitting and to be used for prediction and transfer learning. Ensure that you set the paths for both the train images and mask images in this step. The model is trained on the 4,000 images, and their masks contain the mask labels. The acquired weight is saved to train the whole train dataset. Their folders are available for download in Google Drive under Submission_2_and_1. (The process of generating these folders is available in the preprocessing step notebook.) The order of running the models is reversed. Note: This section does not need to be executed. The finalized models have already been saved and can be found in the "Submission 3" folder on Google Drive, which is shared by the committee. These models will be used for predictions on the 12 test images.

3. Predict the Final Test Set (12 Test Images): A data generator is used to read the tiled test images and make predictions. (The 12 test regions' images are divided into tiles of 512x512 to be used with the model trained on 512x512 image dimensions.) Set the path for the tiled test files in the code. Load the trained model with a line similar to the following: model.load_weights("best_model_lake_512_512_2k_lake_2k_none_res_attention_fold_1.h5").

4. Stitch the Tiled Test Images: Combine the tiled test images and the predicted images to obtain predictions for the 12 regions with their original sizes. Set the path to the JSON folder containing each image's information, including added 0 padding positions in the code. Configure the paths in their code block to stitch predicted images together:

input_folder = "test_tiles_no_overlap"

output_folder = "stitched_tiled_test_images_submission_5"

metadata_folder = "json_test_tiles_no_overlap"

For prediction:
You can download it from submission folder 2 on Google Drive
input_folder = "Final_Predictions/predicted_test_4k_Attention_res_net_2k_lake_2k_no_lake_no_overlap"

output_folder = "stitched_test_prediction_submission_5"

metadata_folder = "json_test_tiles_no_overlap"

5. Align Predicted Images with Original Test Images: Align the coordinates of the 12 stitched predicted images with the 12 original test images. 

6. Post-processing and providing lake_polygons_test.gpkg lake_polygons_test.gpkg: Specify the path for the projected predicted images in the code, similar to test_prediction_dir = "projected_predicted_images_closed_submission_3". Implement any necessary post-processing steps to refine the predictions and achieve the desired output quality. Running the below steps is not necessary.

Sanity Checks: Perform sanity checks to ensure the accuracy and reliability of the predictions. Overlay an extracted region from lake_polygons_test.gpkg with its projected image to verify whether their coordinates are aligned. Also, this is done both before and after creating the test package.

## Citing Our Work
If you use any part of this code, including any of the five solutions, for academic work, research, or any other projects, please cite us. You can use the following BibTeX entry:

```BibTeX
@misc{AtefehJebeli2023lakedetection,
    title={Lake Detection},
    author={Atefeh Jebeli},
    year={2023},
    publisher={GitHub},
    howpublished={\url{https://github.com/AtefehJebeli/Lake_Detection}}
}
