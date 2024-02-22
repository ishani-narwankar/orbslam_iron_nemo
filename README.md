# ORB_SLAM2 Configuration for Nemo AUV Project
This repo includes all of the packages needed and adjusted to work on ros2 iron with camera calibration specifically for my independent research project nemo AUV which you can read more about here: https://github.com/ishani-narwankar/nemo_auv

## Reference Repos
This repo makes use of the ORB_SLAM2 package which can be found here: https://github.com/raulmur/ORB_SLAM2 and the ros2_ORB_SLAM2 package which can be found here: https://github.com/alsora/ros2-ORB_SLAM2/tree/master


## Launch

### Terminal 1
1. source `orbslam` workspace
2. ```ros2 run ros2_orbslam mono ~/ws/orbslam/src/ORB_SLAM2/Vocabulary/ORBvoc.txt ~/ws/orbslam/src/ros2-ORB_SLAM2/src/monocular/[camera config yaml]```
3. once map gui pops up run commands in terminal 2

### Terminal 2
*to run test orbslam on a livestream from laptop camera*

- ```ros2 run image_tools cam2image --device_id 1 --ros-args --remap /image:=/camera```

*to run test orbslam on a rosbag file*

- cd into rosbag folder
- ```ros2 bag play [rosbag file folder] --remap /video_frames:=/camera /camera_info:=/camera/camera_info```

*to run test orbslam on a livestream from realsense camera plugged into laptop*
- `ros2 run realsense2_camera realsense2_camera_node --ros-args --remap /color/image_rect_raw:=/camera`

## Notes
make sure to remap the following topics

- ```/video_frames:=/camera``` (video_frames to camera)
- ```/camera_info:=/camera/camera_info``` (camera_info to camera/camera_info)

## Debugging Notes
The following checks might be helpful for debugging if nothing shows up in the mapping gui:

- `ros2 topic info [topic name]` - to find out what type the topic is and make sure it matches with what ORB_SLAM wants for their `/camera` and `/camera/camera_info topics`

- `ros2 topic echo [topic name]` - echo the remapped topics to see if information is being published on them