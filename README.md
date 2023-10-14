# Lake_Detection
There are 5 different solutions. Each solution notebook with its lake_polygons_test.gpkg and README file is under its submission folder. Also, complementary folders of each solution are uploaded on Google Drive, which is shared with the committee.
Before running each solution completely, you must run mandatory parts of the preprocessing Notebook. Otherwise, the saved model and tiled test folder are available on Google Drive.

Tiling for Consistency: The original extracted regions in our dataset vary in size. To ensure consistency, we tile these regions into 512x512 patches with overlapping sections and zero padding applied as needed. This part is done in preprocessing Notebook. The resulting tiled images are saved in three separate folders: trained_tiles: Tiled images used for training. mask_tiles: Tiled masks associated with the training data. test_tiles_no_overlap: Tiled test images without overlapping sections.

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
