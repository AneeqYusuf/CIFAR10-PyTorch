# CIFAR10-PyTorch
An Implementation of The CIFAR10 Model on PyTorch For Correction Of Facial Orientation

-Basically there are two main files that need to be executed in this code, namely the 'trainer.py' file and the 'output_generator.py' file. 
-Before running any of the files, make sure to adjust the file paths on line 19 (in trainer.py) to the folder containing your trainset images (do not forget the '/' at the end) and the truth csv file for the trainset, respectively.
-File paths in output_generator.py file need to be updated as well, on lines 16, 17, with paths for the folder containing the test images and the folder where you want the updated images to be saved, respectively.

-The trainer.py file trains the CIFAR10 model with four output labels, after normalizing the images (via PyTorch Transforms). These include:
  1.) 'upright'
  2.) 'rotated_left'
  3.) 'rotated_right'
  4.) 'upside_down'
  
Once the model is trained, it is saved as model.sav in the same folder, where your trainer.py was located.

The output_generator.py file makes use of the saved model and passes a set of images through it, to fetch the predicted labels for each image. (Please note that the input images are to be passed as a set of images, through the PyTorch data loader object).

The output_generator then uses these labels to generate a truth file for the test images, as a csv, to verify the results.

The orientations of the images is corrected, based on the predicted label and saved in your specified location, as png files. This is done using OpenCV.

A numpy array for the images test set is also generated and saved for further feeding into any future networks.

The 'net.py' file contains two classes, the network definition class (Net) and the data loading class (data_load).

The data load class allows for defining a custom mechanism for loading images into a set that can be fed to the network. This is also where the transformations are applied to the images.

The Net class contains an initialization function and a feed forward function (with Relu activations). Since the CIFAR10 model was originally designed to predict the labels for 10 different types of images, minor tweaks to the network topology were needed. This included the addition of a new layer, dropping from 10 features to 4 (the number of labels) and the readjustment of the first layer of the linear net (to 2704 nodes), since the size  of the images was 64x64x3, as compared to CIFAR10's original dataset, which was 32x32x3.
