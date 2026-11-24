# Skin Lesion Segmentation

Team project by J Kowshik and K S Vinay Sathvik, completed in the second year of the B.E. in Artificial Intelligence and Machine Learning at B.N.M. Institute of Technology, Bengaluru.

Unsupervised segmentation of dermoscopic images from the Kaggle
[Skin Cancer: Malignant vs. Benign](https://www.kaggle.com/datasets/fanconic/skin-cancer-malignant-vs-benign)
dataset (224 x 224 RGB images, two classes). The notebook separates the lesion from the surrounding skin and crops a region of interest that can be passed to a downstream classifier.

## Pipeline

1. **Data.** Download the dataset with `kagglehub` and index the malignant and benign training images.
2. **Clustering.** Run K-Means on grayscale pixel intensities. The number of clusters is chosen from the elbow curve (k = 2 separates lesion and skin).
3. **Lesion cluster selection.** Take the cluster with the lowest mean intensity as the lesion mask.
4. **Mask refinement.** Smooth the mask with a disk mean filter and binarise it with Otsu's threshold.
5. **ROI extraction.** Multiply the refined mask into each RGB channel, then trim residual border regions by column statistics.
6. **Colour-space variants.** Repeat the clustering on RGB pixel vectors (`cv2.kmeans`) and in L\*a\*b\* space for comparison.
7. **Dataset summary.** Class counts and a resized grayscale export of the malignant images.

## Running

Open `Skin_Cancer_Lesion_Classification.ipynb` on Kaggle or in Google Colab and run the cells in order. The paths assume the Kaggle input layout (`/kaggle/input/skin-cancer-malignant-vs-benign/...`).

Dependencies: `numpy`, `pandas`, `matplotlib`, `scikit-image`, `scikit-learn`, `scipy`, `opencv-python`, `kagglehub`.

## Scope

This is a segmentation and preprocessing study. No classifier is trained, so the notebook does not report malignant/benign accuracy. The extracted regions of interest are intended as input to a supervised model such as a CNN.
