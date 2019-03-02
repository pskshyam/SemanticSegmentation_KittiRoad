# SemanticSegmentation_KittiRoad
Semantic Segmentation of road images in Kitti Road Dataset

## Introduction
Let’s walk through a step-by-step implementation of the most popular architecture for semantic segmentation — the Fully-Convolutional Net (FCN). We’ll implement it using the TensorFlow library in Python 3, along with other dependencies such as Numpy and Scipy.

In this exercise, we will label the pixels of road in images using FCN. We’ll work with the Kitti Road Dataset for road/lane detection.

## Key Features of FCN Architecture
* FCN transfers knowledge from VGG16 to perform semantic segmentation.
* The fully connected layers of VGG16 is converted to fully convolutional layers, using 1x1 convolution. This process produces a class presence heat map in low resolution.
* The upsampling of these low resolution semantic feature maps is done using transposed convolutions (initialized with bilinear interpolation filters).
* At each stage, the upsampling process is further refined by adding features from coarser but higher resolution feature maps from lower layers in VGG16.
* Skip connection is introduced after each convolution block to enable the subsequent block to extract more abstract, class-salient features from the previously pooled features.

## Steps involved in FCN-8 Implementation
There are 3 versions of FCN (FCN-32, FCN-16, FCN-8). We’ll implement FCN-8, as detailed step-by-step below:

* Encoder: A pre-trained VGG16 is used as an encoder. The decoder starts from Layer 7 of VGG16.
* FCN Layer-8: The last fully connected layer of VGG16 is replaced by a 1x1 convolution.
* FCN Layer-9: FCN Layer-8 is upsampled 2 times to match dimensions with Layer 4 of VGG 16, using transposed convolution with parameters: (kernel=(4,4), stride=(2,2), paddding=’same’). After that, a skip connection was added between Layer 4 of VGG16 and FCN Layer-9.
* FCN Layer-10: FCN Layer-9 is upsampled 2 times to match dimensions with Layer 3 of VGG16, using transposed convolution with parameters: (kernel=(4,4), stride=(2,2), paddding=’same’). After that, a skip connection was added between Layer 3 of VGG 16 and FCN Layer-10.
* FCN Layer-11: FCN Layer-10 is upsampled 4 times to match dimensions with input image size so we get the actual image back and depth is equal to number of classes, using transposed convolution with parameters:(kernel=(16,16), stride=(8,8), paddding=’same’).
Steps involved in Semantic Segmentation

## Training Parameters

289 images used in training

289 labels used in training

290 images used in testing

Learning rate = 0.0001

Epochs = 30

Samples per epoch = 100

Batch Size = 8
