# DCGAN-Using-Tensorflow-and-keras---MNIST-simple-example
## Use tensorflow to build and tune a deep convolution generative adversarial network to generate images of hand-written digits from the classic MNIST dataset.
### The idea behind the DCGAN is very simple: Train the genrator and the discriminator using convolutional neural networks.

It is worth noticing that:<br>
1. When building a DCGAN model, the discriminator should not have any feature extracting process like pooling and global pooling because such process will make the discriminator learn the special feature patterns when identifying real and fake images, which is not desirable. We want the discriminator to learn the differences between the distribution of data of real images and that of fake images. Pooling layers will destroy the spatial distribution patterns extracted from the conv layer.

2. It is empirically known that LeakyReLU resulted in better result on the discriminator's performance and learning process because the LeakyReLU further reduces the likelihood of encountering the diminishing gradient problem. But one should be careful when tuning the slope of the LeakyReLU.

3. tanh is a desired activation function for the final output layer of the generator.

4. Learning rate and optimizer play a crucial rule and one should pay additional attention toward tunning them.

5. Because there is no evaluation metric to judge the performance during training, and lower loss does not necessary means bettern performance (in the context of generating images), tunning may be hard. One empirical observaation is that if your model, when generating a batch of images, outputs images that are very similar, that could be a sign of overfitting (the generator remembered some pattern that it considered can fool the discriminator).

6. The discriminator and the generator need to be trained at about the same pace to avoid one dominating another and slow down the learning. To achieve such, I used same optimizers with same hyperparameters for both models.

7. This type of model is extremely computational-heavy because without the pooling layer, the output of the discriminator is much more complicated and the Conv2DTranspose is also heavy. Running on my local device with RTX2060 GPU, 28 * 28 gray scale images are the best I can do. If you want to build a model that can output other complicated images, setup a cloud with strong virtual GPU power or get a better computer...
