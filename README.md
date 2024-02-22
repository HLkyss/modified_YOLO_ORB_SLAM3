来源：https://github.com/YWL0720/YOLO_ORB_SLAM3<br />
原开源代码只给了RGBD的，补充了一下自己使用的双目的，后面再补其他的<br />
双目：<br />
./Examples/Stereo/stereo_tum_vi /home/hl/project/ORB_SLAM3_detailed_comments-master/Vocabulary/ORBvoc.txt /home/hl/project/YOLO_ORB_SLAM3-master/Examples/Stereo/ue_pin.yaml /media/hl/Stuff/ubuntu_share_2/Dataset/ue_pin_fov100/theta0/cam0 /media/hl/Stuff/ubuntu_share_2/Dataset/ue_pin_fov100/theta0/cam1 /media/hl/Stuff/ubuntu_share_2/Dataset/ue_180/time.txt /media/hl/Stuff/ubuntu_share_2/Dataset/ue_pin_fov100/theta0/result/dataset-hik_stereo-traj

<img src="https://github.com/HLkyss/modified_YOLO_ORB_SLAM3/assets/69629475/8cc48db0-8361-4afa-92b7-fc0a09603685" width="900"> <br />

单目：<br />
./Examples/Monocular/mono_euroc ./Vocabulary/ORBvoc.txt ./Examples/Monocular/EuRoC.yaml /media/hl/Stuff/ubuntu_share_2/Dataset/EuRoc/V1_02 ./Examples/Monocular/EuRoC_TimeStamps/V102.txt

<img src="https://github.com/HLkyss/modified_YOLO_ORB_SLAM3/assets/69629475/c1ebf5c7-61eb-4e4b-83f1-d30df6d65d12" width="900"> <br />

***
# YOLO_ORB_SLAM3

**This is an improved version of [ORB-SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3) that adds an object detection module implemented with [YOLOv5](https://github.com/ultralytics/yolov5) to achieve SLAM in dynamic environments.**
- Object Detection
- Dynamic SLAM

<p align="center">
  <img src="Fig.png"/>
  <br>
  <em>Fig 1 : Test with TUM dataset</em>
</p>

## Getting Started
### 0. Prerequisites

We have tested on:

>
> OS = Ubuntu 20.04
> 
> OpenCV = 4.2
> 
> [Eigen3](http://eigen.tuxfamily.org/index.php?title=Main_Page) = 3.3.9
>
> [Pangolin](https://github.com/stevenlovegrove/Pangolin) = 0.5
>
> [ROS](http://wiki.ros.org/ROS/Installation) = Noetic


### 1. Install libtorch

#### Recommended way
You can download the compatible version of libtorch from [Baidu Netdisk](https://pan.baidu.com/s/1DQGM3rt3KTPWtpRK0lu8Fg?pwd=8y4k) 
code: 8y4k,  then
```bash
unzip libtorch.zip
mv libtorch/ PATH/YOLO_ORB_SLAM3/Thirdparty/
```
#### Or you can

```bash
wget https://download.pytorch.org/libtorch/cpu/libtorch-cxx11-abi-shared-with-deps-1.11.0%2Bcpu.zip
unzip libtorch-cxx11-abi-shared-with-deps-1.11.0%2Bcpu.zip
mv libtorch/ PATH/YOLO_ORB_SLAM3/Thirdparty/
```

### 2. Build
```bash
cd YOLO_ORB_SLAM3
chmod +x build.sh
./build.sh
```

Only the rgbd_tum target will be build.

### 3. Build ROS Examples
Add the path including *Examples/ROS/YOLO_ORB_SLAM3* to the ROS_PACKAGE_PATH environment variable. Open .bashrc file:
```bash
gedit ~/.bashrc
```
and add at the end the following line. Replace PATH by the folder where you cloned YOLO_ORB_SLAM3:
```bash
export ROS_PACKAGE_PATH=${ROS_PACKAGE_PATH}:PATH/YOLO_ORB_SLAM3/Examples/ROS
```
Then build
```bash
chmod +x build_ros.sh
./build_ros.sh
```

Only the RGBD target has been improved.

The frequency of camera topic must be lower than 15 Hz.

You can run this command to change the frequency of topic which published by the camera driver. 
```bash
roslaunch YOLO_ORB_SLAM3 camera_topic_remap.launch
```

### 4. Try

#### TUM Dataset

```bash
./Examples/RGB-D/rgbd_tum Vocabulary/ORBvoc.txt Examples/RGB-D/TUMX.yaml PATH_TO_SEQUENCE_FOLDER ASSOCIATIONS_FILE
```

#### ROS

```bash
roslaunch YOLO_ORB_SLAM3 camera_topic_remap.launch
rosrun YOLO_ORB_SLAM3 RGBD PATH_TO_VOCABULARY PATH_TO_SETTINGS_FILE
```

