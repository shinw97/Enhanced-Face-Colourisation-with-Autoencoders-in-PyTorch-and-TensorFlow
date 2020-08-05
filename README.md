# Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras

## Motives
### Colour Restoration on Vintage Photos
We live in an era where **Black and White Photos** are just products of digital effects in modern photography. Yet there are continuous work from historians, vintage art lovers, artists, film producers, or just some random nostalgic person, to recover/restore colours on old photos/films with their respective purposes. 


### Because I have too much time
Yeah, this was just one of my hobby projects I wanted to try out during the COVID-19 pandemic. So... yeah.

## Autoencoders
Image editing softwares are commonly used for the restoration. However, it requires skills and time to complete the task. As the [colourisation video editing tutorial here](https://www.youtube.com/watch?v=7SfTTDIjiM4) shows, it takes almost 18 minutes to colourise one photo for an photo editing expert. 

Instead, autoencoders, as a common neural network architecture used to encode/decode information, might be suitable for the automation of this task. 

![autoencoders](https://upload.wikimedia.org/wikipedia/commons/2/28/Autoencoder_structure.png)

Figure By Chervinskii - Own work, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=45555552

Usual usage of autoencoders is to send in an image as input to an encoder network to output a much smaller and lighter latent space as the original image representation. The retrieval/restoration of the image is through a decoder network, where the latent space representation is passed through the decoder network (usually the inverted form of the encoder) as input, and finally retrieving the original image as the output with minimal loss.

Note that our purpose is to send in a black and white image (or grayscale image) as input and take the colourised image as the output. Thus we just need to do some modifications on the datasets to achieve that besides  building the autoencoders network.

### Datasets
Since this is just a small scale hobby project, I have narrowed the scale of the project to just **faces**. The faces dataset used are available publicly from the [Large-scale CelebFaces Attributes (CelebA) Dataset]([http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html)).

The dataset contains 202,599 images of faces.

### Training
I have included two Google Colab Notebooks with implementations of faces colourisation autoencoders in PyTorch and Tensorflow-Keras respectively. All implementation and training details are available inside the Notebook.

To summarize the implementation, besides constructing the autoencoders network with just simple VGG16 architecture, the training images (black and white photos) are produced by converting all images to grayscale images (X), while the original coloured images act as the ground truth label (y). All images are represented in RGB channels.

After almost an hour of training, the network merely reconstructed the basic shapes, contours and colours of the person from the grayscale image, the output was so blurry and losing all sharp edges.

### Lazier (faster) way to finish the Colorization without spending more Training Time
Well indeed I was too lazy to wait for another few epochs of training for the network to reproduce sharp edges. Why don't we just treat the current outputs of the autoencoders as colour masks for the original grayscale images?

The outputs can be masked or blent with the original grayscale images. By doing this we could preserve the sharp edges besides restoring the colours. 

Some image enhancement techniques can also be done later on the outputs, such as image sharpening filters and HSV management. 
### Sample Outputs
Some other outputs tested:
### Tests on Real Black and White Photos
Well, and this is how the network performed on real black and white photos:
### References for the Images and Diagrams used
