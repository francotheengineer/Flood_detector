# Flood_detector

A computer vision approach to detect flooded areas from aerial imagery.

The aim is to detect areas with flooding and generate a 'patchwork quilt' showing flooded areas to enable better route planning for emergency services.


## Dataset

The dataset for this project can be found here:

This was created using the file *slice_and_crop.ipynb* in *make_datasets* dir. The source data was collected using the search term 'flood imagery' :
<http://qldspatial.information.qld.gov.au/catalogue/custom/search.page>

This yielded these 2 datasets and more:

1. [Flood imagery - Talwood 0.5 metre - January 2011](http://qldspatial.information.qld.gov.au/catalogue/custom/detail.page?fid={8C663175-6148-477E-9A86-E794A4015EAA}) 
2.[Flood imagery - Surat 2 metre - January 2011](http://qldspatial.information.qld.gov.au/catalogue/custom/detail.page?fid={635E0A38-A6DC-43FB-BA30-CDE60DD8F185})
You can download my dataset by making an issues and I will email it to you :) 

## Training

In *training.ipynb* exists code to training a simple CNN. Performance would likely improve with models such as [NASNet](https://arxiv.org/pdf/1707.07012.pdf) or a more simple architecture such as Inception-v3.

I decided to use Keras since it's becoming the Tensorflow default API in TF 2.0! 🎼🔈 Times they are a'changing 🎼🔈
Run this in google colab! I've tested it to make sure it works! Just:

`git clone https://github.com/francotheengineer/Flood_detector.git`
and upload the ipynb to Colab!

## Inference

The idea is to make a colour modified map to show the areas with and without flooding.
I used another image from the QLD Spacial site for inference. 

The output can be seen:

<p align="center">
<img src="DP_BUND_BUNDABERG_NORTH_AP_2011_13CM_lowqual_overlayed.png" width="50%""/>
</p>

Another result before I performed some dataset cleansing:

<p align="center">
<img src="bad_result.png" width="50%""/>
</p>


## Learnings

1. There is a significant colour variation in the colour of the floods. This is the main artefact use to make the dataset. This can be solved with much more training data. <500 images isn't a lot for a full train of a CNN.

2. Some data normalisation could be used:
    `determine flood water colour range -> replace with a narrower range of colour -> do for both train and inference images`
3. Test more modern CNNs such as Inception-V3 and compare results

4. I spent quite some time dealing with the enormous images from the source. This was impossible to deal with in OpenCV due to 2^32 pixel limits. I resized with GIMP then read into OpenCV, change your slicing window accordingly! This flag can also work when the images are lower than the limit but use too much ram: 

```org_image = cv2.imread(image_path, cv2.IMREAD_REDUCED_COLOR_8)```
