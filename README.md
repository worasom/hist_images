# Histopathological Images

Nuclei segmentation of stained tissue images of tumor patients in MICCAI2018 challenge. The data contains about 30 images and a corresponding mask. Use fast.ai and Unet architectures to do nuclei segmentation.

Analysis Procedures:
- Train Unet to perform image segmentation on the 128 pixel images and black&white mask. Predict on the resized 250 or 500 pixel. Details in this [notebook](https://github.com/worasom/hist_images/blob/master/MoNuSeg_fastai_unet-wk.ipynb).
- Work with small dataset. There were only 30 training images. Each has 1000 x 1000 pixels. Generate 125x125 images crop images and mask files (opencv, PIL, imageio, skimage). Up sample to 128 pixel image. Details in this [notebook](https://github.com/worasom/hist_images/blob/master/MoNuSeg_resize.ipynb).
- Accuracy 90% on the validation set 

# Data Preparation

When training a neural network, I often have to resize the image to a smaller images about 128 pixels. In this case, it also help generate more images for training.

In the data preparation step, I cropped image and the mask images into 500 pixels image save them in the 500 pixels folder. Then crop these images into 250 pixel images folder, then to 125 images folder. Then, I upsample the 125 images to 128 pixels. The reason from not jumping straight from 1000 to 128 folder directly, is because I want to work with different images sizes; for example starting training NN using the 128 pixels, then 250, 500 images.

**Tissue Image***

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig2.png)

**Mask Image***

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig1.png)

## Preparing Mask Files

In order to convert color mask image to black and white. I first convert the three channel images to a gray scale image and use thresholding to convert to a binary image. 

**Original Mask Image**

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig3.png)

**Mask Image in Gray-scale**

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig4.png)

**Binary Mask Image**

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig5.png)

**Mask Image After Cropping to 128 pixel and Converted to Black and White**
![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig6.png)

## Nuclear Segmentation 

Train Unet to perform image segmentation on the 128 pixel images and black&white mask. Predict on the resized 250 pixel images. Then train on the 250 pixel images and predict on the resize 500 images

**Overlaying128 pixes mask files on the tissue images **

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig7.png)

### Training UNET on cropped 128 pixel images.

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig8.png)

This is the result on the validation set. 

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig9.png)

The CNN seems to do pretty good job of segmentation the resized 250 pixels and 500 pixel images with  about 90% accuracy. However, the model does not do well on 1000 pixels images.

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig11.png)

### Training UNET on cropped 500 pixel images.

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig12.png)

We obtained about 88% accuracy on the validation sets on 500 pixel images. However, the model still perform poorly on the 1000 pixels, as seen below. I also ran into memory problem during the training, even with a smaller batch size. 

![](https://github.com/worasom/hist_images/blob/master/gitfigures/fig13.png)


# Summary,

In this project, I performed nuclei segmentation of stained tissue images. A small data set and large image size is a huge challenge in this problem. Insteading of resizing image, I cropped the image instead. UNET is still able to segment nuclei eventhough it used to see a larger nuclei. 
