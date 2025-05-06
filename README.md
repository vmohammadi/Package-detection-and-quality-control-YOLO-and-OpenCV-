# Package-detection-and-quality-control-YOLO-and-OpenCV-

## Train YOLOv8 on a custom dataset
First, you may go to the file named "custom_train_yolov8.ipynb" for training your YOLO. In this file, I used version 8 of YOLO and trained it on a custom dataset. I preferred to train it on a custom dataset because in many projects, there is no dataset on the precise product in question. The dataset that I used is a small synthetic dataset of medicine boxes, found on several websites including Roboflow:

https://universe.roboflow.com/new-workspace-uouq3/package-quality-control

It is noted that you need to perform labelling either with a tool like YoloLabel or Roboflow. Also, be sure you arrange the folder tree correctly and create a yaml file.
The goal then is to train the YOLO on the dataset and save the best model for the control program. In the control program only you call the model to find the object in the image.

## Quality control
You can perform the quality control with different techniques, either deep learning or image processing. I preferred to perform this by using image processing to have both deep learning and image processing in the project. To do so, please refer to "quality_control.ipynb". Here is an overall diagram of the processing:

![Diagram](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/dia.png)

First we call the trained YOLO to find the object. This is necessary as the box can appear anywhere in the image. Then, we check the edges of the box. We see that the box is damaged if the edges are not straight, and then the box should be ejected out of production line.

![im1](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/0.the%20edges.png)

So, after doing object detection with our YOLO, we take the coordinates of the frame around the detected box (ROI) and extract it.

![im2](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/1.get%20the%20ROI.png)

Then, we need to extract the green part as a binary mask. This is quite optional to choose which part of the box you would like to consider for defect detection. We could even take the white part. However, I only extract the green part and it is enough for this quality control task. In case of having more complicated defects, you may need to add other steps of processing. For the extraction of the green part, I took benefit of HSV color space.

![im3](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/2.get%20mask.png)

Finally, we check the horizontal edges if they are straight or not. If they are curvature or broken, it means that the box is damaged. I note that I check the horizontal edges and I did not consider vertical edges as normally the defects apear on the horizontal edges. In the program you can control the precision of the algorithm. You can adjust the amount of acceptable deviation from the straight line and the minimum length of edges to be considered. Also, you may need to change Epsilon in the body of function "detect_edge_defects" which is in charge of the maximum distance from the contour of the binary mask to the approximated contour.

![im4](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/3.control.png)

### Some examples of the control

![im5](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex1.png)

![im6](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex3.png)

![im7](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex2.png)

![im8](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex4.png)
