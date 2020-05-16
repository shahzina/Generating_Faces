# Generating_Faces
Using celebrity image data to generate new faces using DCGANs

## What are DCGANs?? <br>
GANs or Generative Adversarial Networks are generative models that generate images one pixel at a time. To generate our fake images we will be using convolutional layers, which is why are model is called a Deep Convolutional Generative Adversarial Network or DCGAN. <br>

## Steps involved:- <br>
### 1- Loading and pre-processing Images <br>
Some pre-processing has already been done in the given dataset while a lot more needed to be done. We start by defining our **get_dataloader** function which returns a data loader after applying various transformations. <br>

First, we define our transformations we want to apply using the *transforms.Compose* method provided by PyTorch. Here, we have resized our image to *image_size* which we have assigned a value of 32 and then converted this Numpy image to a Tensor. <br>
Then we use the *ImageFolder* wrapper to create a dataset and apply the defined transformations. The ImageFolder wrapper is used here to create a dataset of the directory of images. <br> 
Then we create our data loader using PyTorch's *DataLoader* and pass in our transformed dataset and batch size and shuffle values. <br> 

We also scale our images as they are currently between 0 and 1 while the generator will yield images between -1 and 1 because a tanh activation is applied to the output layer of a generator. <br>

### 2- Model Definition - Discriminator <br>

### 3- Model Definition - Generator <br> 

### 4- Weight Initialization <br>

### 5- Building the complete model <br> 

### 6- Define Loss Functions and Optimizers <br> 

### 7- Train <br> 
![training loss](https://github.com/shahzina/Generating_Faces/blob/master/img_dcgan/training%20loss.png)

### 8- Display Samples <br>
![generated images](https://github.com/shahzina/Generating_Faces/blob/master/img_dcgan/generated%20images.png)


## Comments on Final Results <br> 
