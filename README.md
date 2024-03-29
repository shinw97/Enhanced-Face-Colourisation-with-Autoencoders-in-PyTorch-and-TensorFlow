
# Enhanced-Faces-Colourisation-with-Autoencoders-in-PyTorch-and-TensorFlow
<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/assets/Intro.png?raw=true" width="60%"/>
</p>

## Motivations
### Automated Colour Restoration on Vintage Photos
We live in an era where **Black and White Photos** are just the products of digital effects in the modern photography. Yet there are a lot of continuous effort from the historians, vintage art lovers, artists, film producers, or just some random nostalgic person, to try to recover/restore the colours on the old photos/films. 

### Because I have too much time
Yeah, this was one of my hobby projects I wanted to try out during the COVID-19 pandemic. So... yeah.

## Autoencoders
Image editing softwares are commonly used for the image restoration task. However, it requires skills and time to complete the task. It can take minutes to colourise one photo for a photo editing expert. 

Instead, autoencoders, as a common neural network architecture usually used to encode/decode image information, might be suitable to automate this task. 

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/2/28/Autoencoder_structure.png" width="60%"/>
!<p align="center">Figure By Chervinskii - Own work, CC BY-SA 4.0, <a href="https://commons.wikimedia.org/w/index.php?curid=45555552"> https://commons.wikimedia.org/w/index.php?curid=45555552</a>
</p>
</p>

The usual usage of the autoencoders is to perform dimensionality reduction on the vector data for lighter transmission or storage. 

An image is first sent in as input to the encoder network to get a much smaller and lighter latent space as the representation of the original image. Then, the retrieval/restoration of the image is through a decoder network (usually the inverted form of the encoder), where the latent space representation is passed through as the input, and finally retrieving the original image as the output with minimal loss.

Note that our purpose is to send in a black and white image (or grayscale image) as input and take the colourised image as the output. Thus, we just need to do some modifications on the datasets to achieve that besides building the autoencoders network.

### Datasets
Since this is just a small-scale hobby project, I have narrowed down the scale of the project to just **faces**. The faces dataset used are available publicly from the [Large-scale CelebFaces Attributes (CelebA) Dataset](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html).
<p align="center">
<img src="http://mmlab.ie.cuhk.edu.hk/projects/CelebA/intro.png" width="60%"/>
<p align="center">The dataset contains 202,599 images of faces.
</p>
</p>


### Training
I have included two Google Colab Notebooks with the implementations of the face colourisation autoencoders in PyTorch and Tensorflow-Keras respectively. All implementation and training details are available inside the Notebook.

To summarize the implementation, besides constructing the autoencoders network with just a simple VGG16 architecture, the training images (black and white photos) are produced by converting all the images to grayscale images (X), while the original coloured images act as the ground truth label (y). All images are represented in RGB channels.

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/assets/convert-grayscale.png?raw=true" width="60%"/>
</p>

After an hour or more of training, the network merely reconstructed the basic shapes, contours and colours of the person from the grayscale image, the output was blurry and losing all the sharp edges.

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/assets/net-output.png?raw=true" width="25%"/>
</p>

## What about a Lazier (faster) way to finish the Colourisation without spending more Training Time?
Well indeed I was too lazy to wait for another few epochs of training for the network to reproduce sharp edges. Why don't we just treat the current outputs of the autoencoders as the colour masks for the original grayscale images?

The outputs can be masked or blent with the original grayscale images. By doing this we can preserve the sharp edges in the mean time restore the colours. 

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/assets/blended.png?raw=true" width="75%"/>
</p>

Some image enhancement techniques can also be done later on the outputs, such as the image sharpening filters and HSV management. 

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/assets/enhanced.png?raw=true" width="75%"/>
</p>

### Sample Outputs
Some other outputs tested:

<p align="center">
<img src=https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/sample-2.png?raw=true" width="100%"/>
</p>

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/sample-3.png?raw=true" width="100%"/>
</p>

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/sample-4.png?raw=true" width="100%"/>
</p>

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/sample-5.png?raw=true" width="100%"/>
</p>

### Tests on Real Black and White Photos
And this is how the network performed on real black and white photos:

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/real-case-sample-1.png?raw=true" width="100%"/>
</p>

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/real-case-sample-2.png?raw=true" width="100%"/>
</p>

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/real-case-sample-3.png?raw=true" width="100%"/>
</p>

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/real-case-sample-4.png?raw=true" width="100%"/>
</p>

<p align="center">
<img src="https://github.com/shinw97/Faces-Colourisation-using-Autoencoders-in-PyTorch-and-TensorFlow-Keras/blob/master/sample-outputs/real-case-sample-5.png?raw=true" width="100%"/>
</p>

## References for the Images used besides of the Dataset

 1. [https://www.flickr.com/photos/29185076@N05/4591829922/](https://www.flickr.com/photos/29185076@N05/4591829922/)
 2. [https://commons.wikimedia.org/wiki/File:Jfk2.jpg](https://commons.wikimedia.org/wiki/File:Jfk2.jpg)
 3. [https://commons.wikimedia.org/wiki/File:Hermann_Rorschach_c.1910.JPG](https://commons.wikimedia.org/wiki/File:Hermann_Rorschach_c.1910.JPG)
 4. [https://commons.wikimedia.org/wiki/File:Frida_Kahlo,_by_Guillermo_Kahlo_2.jpg](https://commons.wikimedia.org/wiki/File:Frida_Kahlo,_by_Guillermo_Kahlo_2.jpg)
 5. [https://digital-photography-school.com/7-tips-for-black-and-white-portrait-photography/](https://digital-photography-school.com/7-tips-for-black-and-white-portrait-photography/)
