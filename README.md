# Package-detection-and-quality-control-YOLO-and-OpenCV-

## Train YOLOv8 on a custom dataset
First, you may go the file named "custom_train_yolov8.ipynb" for training your YOLO. In this file, I used version 8 of YOLO and trained it on a custom dataset. I prefered to train it on a custom dataset because in many projects, there is no dataset on the precise product in question. The dataset that I used is a small synthetic dataset of medicine box, found on several websites including Roboflow:

https://universe.roboflow.com/new-workspace-uouq3/package-quality-control

It is noted that you need to perform labelling either with a tool like YoloLabel or Roboflow. Also, be sure you arrange the folder tree correctly and create a yaml file.

## Quality control
You can perform the quality control with different techniques, either deep learning or image processing. I preferred to perform this by using both. To do so, please refer to "quality_control.ipynb". First we call the trained YOLO to find the object. This is necessary as the box can appear anywhere in the image. Then, we check the edges of the box. We see that if the edges are not straight, the box is damaged and should be ejected out of production line.

![im1](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/0.the%20edges.png)

Next, we take the coordinates of the frame around the detected box and extract it.

![im2](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/1.get%20the%20ROI.png)

Then, we need to extract green part as a binary mask. This is quite optional to choose which part of the box. We could even take the white part. However, I only extract the green part and it is enough for this quality control task. In case of having more complicated defects, you may need to add other steps of processing.

![im3](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/2.get%20mask.png)

Finally, we check the horizontal edges if they are straight or not. If they are curvature or broken, it means that the box is damaged.

![im4](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/3.control.png)

### Some examples of the control

![im5](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex1.png)

![im6](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex3.png)

![im7](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex2.png)

![im8](https://github.com/vmohammadi/Package-detection-and-quality-control-YOLO-and-OpenCV-/blob/main/otherFiles/Ex4.png)
