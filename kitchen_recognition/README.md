# kitchen recognition
I will implement recognitions necessary  for kitchen work.  

## Table Top
We can use tabletop recognition for kitchentop　object recognition on in 3D Vision.  

### how to run sample

```
roscore
```
```
cd ~/Desktop/codes/in_jsk/my_dataset/rosbag/record-test/
rosbag play tomato-and-onion-2020-05-20-16-19-40.bag -l
```
```
source ~/ros/jsk_demo_ws/devel/setup.bash
roslaunch kitchen_recognition tabletop_test.launch
```

### how to run vegs sample with coral
before run set Coral TPU to USB port!  
launch tabletop recognition for vegs
```
source ~/ros/jsk_demo_ws/devel/setup.bash
roslaunch kitchen_recognition tabletop_test_vegs_bags.launch
```
launch for reconstruct point cloud
```
source ~/ros/jsk_demo_ws/devel/setup.bash
roslaunch kitchen_recognition depth2ptcloud.launch gui:=false
```
launch of object detection of Coral
```
source ~/coral_ws/devel/setup.bash
roslaunch curry_detector_ros edgetpu_vegs_detector.launch INPUT_IMAGE:=/camera/rgb/image_raw
```
play rosbags
```
 cd ~/Desktop/rosbags/vegs_data/
 rosbag play vegs_test.bag -l
```
subscribe `/edgetpu_object_detector/output/image`
```
rosrun image_view image_view image:=/edgetpu_object_detector/output/image
```

## PointPoseExtractor
We can use [PointPoseExtractor](https://jsk-docs.readthedocs.io/projects/jsk_recognition/en/latest/jsk_perception/nodes/point_pose_extractor.html) for
template matching using SIFT features

### sample with video
curry roux sample

#### setup
```
cd catkin_ws/src
git clone https://github.com/ros-drivers/video_stream_opencv.git
catkin build video_stream_opencv
```

#### run sample
PointPoseExtractor launch for curry roux
```
roslaunch kitchen_recognition roux_point_pose_extractor.launch
```
video launch
```
roslaunch kitchen_recognition roux_video.launch
```

play rosbag for camera info
```
cd ~/Desktop/rosbags/
rosbag play compressed_long_test.bag -l
```

### sample with rosbag
PointPoseExtractor launch
```
roslaunch kitchen_recognition point_pose_extractor.launch
```
decompress launch
```
roslaunch kitchen_recognition depth2ptcloud.launch
```
play rosbag
```
rosbag play switch.bag -l
```
