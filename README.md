# Histopathological Images

Collection of works on pathological images: 

1. Nuclei segmentation of stained tissue images of tumor patients in MICCAI2018 challenge.
  * Work with small dataset. There were only 30 training images. Each has 1000 x 100 pixels. Generate 125x125 images crop images and mask files (opencv, PIL, imageio, skimage). Up sample to 128 pixel image. Details in this [notebook](https://github.com/worasom/hist_images/blob/master/MoNuSeg_resize.ipynb).
  * Train Unet to perform image segmentation on the 128 pixel images and black&white mask. Predict on the resized 250 or 500 pixel. Details in this [notebook](https://github.com/worasom/hist_images/blob/master/MoNuSeg_fastai_unet-wk.ipynb).
 
