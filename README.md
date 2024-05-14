# CIFAR-10-Image-Classification

The goal of this project is to implement a Neural Network to predict the image content with a desired architecture.
# Basic architecture
The architecture is composed of a sequence of intermediate blocks B1, B2, . . . , BK that are followed by an output block O, as shown in the following figure. These blocks are detailed in the following subsections.

![image](https://github.com/dibahk/CIFAR-10-Image-Classification/assets/98983201/c718381b-467d-4fd4-8c44-aa07f13c461c)

##2.1 Intermediate block 

An intermediate block receives an image x and outputs an image x′ . Each block has L independent convolutional layers. Each convolutional layer Cl in a block receives the input image x and outputs an image Cl(x). Each oft hese images is combined into the single output image x′, which is given by

$x′ = a1C1(x) + a2C2(x) + . . . + aLCL(x)$

where $a = [a1, a2, . . . , aL]^T$ is a vector that is also computed by the block. Note that each convolutional layer in a block receives the same input image x (and not the output of another convolutional layer within the block)

Suppose that the input image x has c channels each channel of *x* is computed and stored into a c-dimensional vector m. The vector m is the input to a fully connected layer that outputs the vector a. Note that this fully connected layer should have as many units as there are convolutional layers in the block.
Each block in the basic architecture may have a different number of convolutional layers, and each convolutional
layer may have different hyperparameters (within or across blocks). However, every convolutional layer
within a block should output an image with the same shape.
2.2 Output block
The output block receives an image x (output of the last intermediate block) and outputs a logits vector o.
Suppose that the input image x has c channels. In order to compute the vector o, the average value of each
channel of x is computed and stored into a c-dimensional vector m. The vector m is the input to a sequence of
zero or more fully connected layer(s) that output the vector o.

