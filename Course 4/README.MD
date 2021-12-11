# Convolutional Neural Networks:

## Classic Networks:
VGG, LeNet-5, ALexNet
As you go deeper Nh, Nw decrease and Nc increases(no. of channels)

Note:
Whenever someone talks about linear operation in the context of nns, it's simply:
Z[l+1] = W[l+1]a[l] + b[l+1].

## ResNets:
A Reisdual nn ensures that adding more layers does not affect the accuracy of the nn.
a[l+2] = g(z[l+2] + a[l])
z[l+2] = W[l+2]a[l+1] + b[l+2]

It allows gradients to propogate backward more efficiently.

If we use L2 regularization, and W[l+2] and b[l+2] = 0, then you get a[l+2] = a[l]. Hence, this identity function is very easy for the ResNet to learn. 

Also, z[l+2] and a[l] must have the same dimension. Hence, "same" convolutions are widely seen in ResNets. 
"same" convolution is where the padding and stride are set such that after the convolution Nh = Nh-1 and Nw = Nw-1.

Or, a[l+2] = g(z[l+2] + W * a[l])
Here W can be learned or it can be a fixed matrix to adjust the dimensions of a[l] so that it matches that of z[l+2]. 

Having ResNet blocks with the shortcut also makes it very easy for one of the blocks to learn an identity function. This means that you can stack on additional ResNet blocks with little risk of harming training set performance. Skip connections send information to every upsampling layer in the decoder from the corresponding downsampling layer in the encoder, capturing finer information while also keeping computation low. These help prevent information loss, as well as model overfitting.

## 1X1 Convolution:
The effect of a one-by-one convolution is it just has nonlinearity. It allows you to learn a more complex function of your network by adding another layer. Also it can be useful to reduce computation by using it to decrease the no. of channels. For e.g. 28x28x192 -> 28x28x32 using 1x1x192 kernel.

## Inception Net:
Uses 1x1 convolutions to reduce the computations for convolving large kernels.

## Mobile Net:
Used for computer vision on devices with low compute. Uses depth-wise convolution.

## Transfer Learning:
Freeze the base model i.e. the pretrained weights and biases must not change. Only the added FC and softmax layer params should be learned.

## Sliding Windows:


## YOLO:
You assign an object to a grid cell if the midpoint of that object lies within that cell. Even if the object spans multiple grid cells, during labelling it must be assigned to the cell that contains the midpoint.
Target output of convnet of YOLO algorithm:
NxNxC
NXN -> no. of grid cells the image is divided into
i.e. width divided into N parts and height divided into N parts
C -> channels
the C channels represent:
pc, bx, by, bh, bw, c1, c2, c3...
pc = 1 if one of the classes is detected in the cell. 
pc = 0 if no class is detected.. all other values are now "don't care"
This is for labelling, for output it is the probability that one of the classes is in the cell
bx, by -> midpoint/center of the detected object
bh, bw -> height and width of the bounding box
c1,c2.. cn -> the bit is one if the object detected belongs to the corresponding class.

** bx,by are assigned relative to the grid cell and not the entire image. the top left corner of the grid cell is taken as (0,0) and the bottom right as (1,1).

YOLO works very fast, even real time detection as effectively there is just a single ConvNet that is doing all the computations for a single input image.

## Non-Max Suppression:
The bounding box with the highest prob is highlighted and every other bounding box with a high intersection over union(IoU) is suppressed.

## Region Proposals/ R-CNN:
Propose Regions(usually done using semantic segmentation), Classify regions one at a time. Output label + bounding box.

## Semantic Segmentation:
The goal is to draw a careful outline around the object that is detected so that you know exactly which pixels belong to the object and which pixels don't.

## One Shot Learning:
Learning from one example to recognize the person again.
d(img1,img2) is the degree of difference between two images. So if we can train the d() function we can address oneshot learning where the input to our model will be two images and the function returns whether the two images are from the same person or not.

## Important links for dl in general:
1. https://towardsdatascience.com/deep-learning-which-loss-and-activation-functions-should-i-use-ac02f1c56aa8
2. https://machinelearningmastery.com/how-to-visualize-filters-and-feature-maps-in-convolutional-neural-networks/
3. Notes: https://github.com/gmortuza/Deep-Learning-Specialization