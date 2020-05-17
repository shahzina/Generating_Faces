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
The discriminator, as the name suggests, discriminates between the images, meaning it determines whether the image generated by the generator is real or fake. <br>

The discriminator is a convolutional neural network with one fully connected layer at the end. It takes in an image and determines whether it is real or fake. This convolutional network, unlike others, does not have a maxpooling layer and the downsizing is done using a stride of 2. It does however use batch normalization in some layers and a leaky relu activation. Leaky relu prevents the nodes of a neural network from dying during dropout and batch normalization scales the layer's output to have a mean of 0 and variance of 1 (defined in the *weights_init_normal* function later. This helps the network train faster. <br> 

When training a discriminator, half the time it is trained on real images and the other half on fake images so that it learns to know the difference between both and output the correct probability. <br>

### 3- Model Definition - Generator <br> 
As suggested by the name, the generator generates realistic fake images. The aim of the generator is to fool the discriminator into predicting that the generated image is real instead of fake.It does this by understanding and learning the underlying structure of the training data. <br>

The generator model is a transposed convolutional model, meaning it starts with the fully connected layer and works it's way to a bigger image of desired size. It takes in a vector z which is filled with random noise values and it's task is to map this random noise to an output x. This mapping is done based on what the generator learns from the training data. In our model we start with a fully connected layer and move to convolutional layers with a stride of 2, therefore, each image is upsampled by 2 in every layer and the depth is decreasing. The last layer does not use any leaky relu or batch normalization, instead we apply a tanh activation function. <br>

### 4- Weight Initialization <br>
The weights have been initialized as described in the [original DCGAN paper](https://arxiv.org/pdf/1511.06434.pdf, i.e. from a zero-centered mean and standard deviation 0.02. The bias terms have been initialized to 0 but this is optional. <br>

The weight initialization function has been defined as shown in the [PyTorch DCGAN tutorial](https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html#weight-initialization) <br>

### 5- Building the complete model <br> 

### 6- Define Loss Functions and Optimizers <br> 

### 7- Train <br> 
![training loss](https://github.com/shahzina/Generating_Faces/blob/master/img_dcgan/training%20loss.png)

### 8- Display Samples <br>
![generated images](https://github.com/shahzina/Generating_Faces/blob/master/img_dcgan/generated%20images.png)


## Comments on Final Results: <br> 
The generated images resemble normal human faces but many features need work and need to be learnt better by the model. Building a deeper model will help in better learning the features. Non-celebrity faces can also be added to the dataset with proportional representation of most or major ethnic groups. <br>

The model can also be trained for more number of epochs, but if the model is deep enough, 50 epochs is a good enough number for it to learn. <br> 

Normalization techniques can also be used for better image resolution. <br>
