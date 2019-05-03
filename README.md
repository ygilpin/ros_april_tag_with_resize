# ros_april_tag_with_resize
This package april_resize subscribes to an image stream topic (provided by usb_cam) and then publishes a smaller version of it.
ROS Indigo
# Dependencies 
1) [usb_cam](http://wiki.ros.org/usb_cam)
2) [april_tags](http://wiki.ros.org/apriltags_ros) 
3) [image_proc](http://wiki.ros.org/image_proc)

# Camera Calibration
This significantly improves results, but is not requried. 
1) It is important to calibrate your camera so that the april tag library can determine its relative position from the image alone. 
2) The ROS [camera_calibration](http://wiki.ros.org/camera_calibration) package works well. After downloading the package, follow the [instructions](http://wiki.ros.org/camera_calibration/Tutorials/MonocularCalibration). Depending on setup an example process flow might be: 
3) `roslaunch usb_cam usb_cam-test.launch &`
4) `rosrun camera_calibration cameracalibrator.py --size 8x6 --square 0.0254 image:=/usb_cam?image_raw camera:=/usb_cam`
5) The calibration data is by default stored in `/tmp`
6) Extract using `tar xfv ...` 
7) Put the .yaml file where the april_tag package expects it `mv ost.yaml /home/ubuntu/.ros/camera_info/`
8) Change the camera_name parameter from narrow_stereo to head_camera and rename the file:
  `cat ost.yaml | sed -E 's/camera_name:.*$/camera_name: head_camera > head_camera.yaml`
# Usage
1) Install this repository and the associated dependencies
2) Put a camera calibration in the default location camera URL. 
For example `/home/ubuntu/.ros/camera_info/head_camera.yaml`
3) Launch the demo.launch file
