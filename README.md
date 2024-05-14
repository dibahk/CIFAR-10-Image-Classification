# CIFAR-10-Image-Classification

The goal of this project is to implement a Neural Network to predict the image content with a desired architecture.
# Basic architecture
The architecture is composed of a sequence of intermediate blocks B1, B2, . . . , BK that are followed by an output block O, as shown in the following figure. These blocks are detailed in the following subsections.

<img src="![image](https://github.com/dibahk/CIFAR-10-Image-Classification/assets/98983201/c718381b-467d-4fd4-8c44-aa07f13c461c)" width="100" height="200">

![image](https://github.com/dibahk/CIFAR-10-Image-Classification/assets/98983201/c718381b-467d-4fd4-8c44-aa07f13c461c) 

## Intermediate block 

An intermediate block receives an image x and outputs an image x′ . Each block has L independent convolutional layers. Each convolutional layer Cl in a block receives the input image x and outputs an image Cl(x). Each oft hese images is combined into the single output image x′, which is given by

$x′ = a_1C_1(x) + a_2C_2(x) + . . . + a_LC_L(x)$

where $a = [a_1, a_2, . . . , a_L]^T$ is a vector that is also computed by the block. Note that each convolutional layer in a block receives the same input image x (and not the output of another convolutional layer within the block)

Suppose that the input image x has c channels each channel of *x* is computed and stored into a *c-dimensional* vector m. The vector m is the input to a fully connected layer that outputs the vector **a**. Note that this fully connected layer should have as many units as there are convolutional layers in the block.
Each block in the basic architecture may have a different number of convolutional layers, and each convolutional
layer may have different hyperparameters (within or across blocks). However, every convolutional layer
within a block should output an image with the same shape.

## Output block

The output block receives an image *x* (output of the last intermediate block) and outputs a logits vector **o**. Suppose that the input image *x* has c channels. In order to compute the vector **o**, the average value of each channel of *x* is computed and stored into a c-dimensional vector **m**. The vector **m** is the input to a sequence of zero or more fully connected layer(s) that output the vector **o**.

# Implemented architecture

## Intermediate Blocks

The model that was employed in this project has 4 intermediate blocks and each block is consisted of 3 parallel Convolutional layers. In all the layers the padding is set as *‘same’* so that the input and output will have the same. In order to use *‘same’* it was required to set the value of stride as 1. Therefore, no alternation has been done on stride and padding. The set up of each block is as followed in the table below. The number of input and output channels has been inspired by VGG16.

| Table | Num. Layers | Kernel 1 | Kernel 2 | Kernel 3 | In channels | Out channels |
|-------|-------------|----------|----------|----------|-------------|--------------|
| 1     | 3           | 1        | 3        | 5        | 3           | 16           |
| 2     | 3           | 1        | 3        | 5        | 16          | 32           |
| 3     | 3           | 1        | 3        | 5        | 32          | 64           |
| 4     | 3           | 1        | 3        | 5        | 64          | 128          |

## Final model

The class defined for the output block is called “FinalModel”. In this class, the class defined for creating intermediate blocks is used to create the intermediate blocks. For using these blocks sequentially nn.Sequential is used so that the output of each block will be an input of the next.

After going through the intermediate blocks, the average results of each channel will be processed by two fully connected layers. The output of these layers should have the same number of channels as the classes in our dataset, which in this case is 10.

# Final result

The best accuracy achieved by this model is **96.708%** for training dataset and for this training accuracy the test accuracy is **85.31%**.
The figures for cross entropy loss for each training batch and train and test accuracy for epochs are also shown respectively.

![image](https://github.com/dibahk/CIFAR-10-Image-Classification/assets/98983201/2f8a237b-d4ac-42f3-8c0c-8a14cffa2a05)

<img src="<![image](https://github.com/dibahk/CIFAR-10-Image-Classification/assets/98983201/b8fea5d2-2dda-409a-9ffb-d8e3b3893cef)


![image](https://github.com/dibahk/CIFAR-10-Image-Classification/assets/98983201/55fa5a62-451b-44dd-9233-43264395cf68)


