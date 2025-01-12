# WorkSafe-ML

WorkSafe-ML is a project that aims to classify if people are wearing their safety gear correctly in fields like chemistry labs, health care and more.
We initially start out with a model that can classify what kind of safety gear is being worn. 


- idea to start out
1. Data Gathering and Annotation
2. Label Bounding Boxes
3. Split the Dataset into Train and Test sets

## Computer Vision: Using ML with the involvement of cameras.

## CNN Model
- Quick Summary

1. Input Image ex: (1,28,28) where 1 is the channels, 28 is the height and 28 is the width. (initial feature map)
2. Convolutional Layer: The amount of filters will be the amount of channels in the next layer.
3. The filter can be seen as a matrix of weights that are applied to the input image. (kernel size is the size of the filter)
4. a filter is applied to the input image and the output is a feature map 
- (original image size - kernel size + 1) is the height and width of the feature map. while amount of filters applied at the channels for the next layer.
- after appling this we get the next layer which is called the feature map 
5. Pooling Layer: This is used to reduce the size of the feature map. (usually a 2x2 filter, but can be different, this is to help against rotations)
6. Flattening: This is to make the data 1D so that it can be fed into a fully connected layer.
7. Fully connected layer will then use MLP method to classify the image, at the end 



## R-CNN Model

- 1. Regional Proposal (Selective Search) 2000 candidate regions
- 2. Crop + CNN for Each Region (Crop the image so that region is resixed into fixed and run a CNN) ConvNet
- 3. We do classification converting to a feature vector and feed to VM for classification, we also generate the bounding box.

## Fast R-CNN Model
- Puts full image through CNN then in feature space you have region propsal method.
- then resize them
- goes through a fully connected layer and linear regression to get the bounding box.
- linear + softmax for classification, probability of each class. 
- Still not fast enough, so we use Faster R-CNN

## Faster R-CNN Model
- Key difference is Region Proposal Network. (RPN)
- R-CNN and Fast-CNN use selective search
1. Image goes through CNN, initially a feature map.
2. Seperate network is for region proposal. 
- Region Proposal Network: 
3. The predicted regions are reshaped and fed into the classifer to predict the object class and bounding box


## Mask R-CNN Model. 
- Object Detection + Segmentation (Instance Segmentation)

- Object Detection: It detects objects in an image using bounding boxes
- Approach to Semantic segmentation: Ie creating a pixel-wise mask for each object
- (assign an object class to each pixel so mapping out the object)

1. We determine the bounding box of object using Faster R-CNN
- Some notes Pooling is for downsizing, Stride is the amount of pixels we move the filter by. 
- We use ROI Align, 
- Stride being quantized is 

## YOLO Model
- Object Localization: Class + Bounding Box
- Pc: Probability of object
- Bx, By, Bw, Bh: Bounding Box x, y are center w,h are height and width
- C1, C2, C3: Class

## Steps:
1. Split the image into grid cells (ex 4x4)
2. For each grid cell, we can predict the bounding box and class. [Pc, Bx, By, Bw, Bh, C1, C2, C3]
- PC is the probability of that object being in that grid cell.
- Each coordinate is normalized between 0 and 1 between the grid cell.

## YOLO learns by
- multi part loss that penalizes (x,y,w,h) mistakes
- confidence errors where box with high confidence doesn't contain an object
- classification errors

## Non-Max Suppression:
- YOLO outputs multiple bounding boxes per grid cell, and many may overlap or be duplicates.
- NMS is applied
1. Sort the boxes by confidence score
2. Select the box with highest confidence score
3. Remove any boxes that have high IOU with the selected box.
4. Yields the final set of detections with minimal overlap.
- Note: For all boxes for a specific class we try to find overlap. 
