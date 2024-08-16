# Camera Configuration

## Step 1: [Install the latest Intel® RealSense™ SDK 2.0](https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md#installing-the-packages)

### Installing the packages:

- Register the server's public key:
```
sudo mkdir -p /etc/apt/keyrings
curl -sSf https://librealsense.intel.com/Debian/librealsense.pgp | sudo tee /etc/apt/keyrings/librealsense.pgp > /dev/null
```

- Make sure apt HTTPS support is installed:
`sudo apt-get install apt-transport-https`

- Add the server to the list of repositories:
```
echo "deb [signed-by=/etc/apt/keyrings/librealsense.pgp] https://librealsense.intel.com/Debian/apt-repo `lsb_release -cs` main" | \
sudo tee /etc/apt/sources.list.d/librealsense.list
sudo apt-get update
```

- Install the libraries (see section below if upgrading packages):  
  `sudo apt-get install librealsense2-dkms`  
  `sudo apt-get install librealsense2-utils`  
  The above two lines will deploy librealsense2 udev rules, build and activate kernel modules, runtime library and executable demos and tools.  

- Optionally install the developer and debug packages:  
  `sudo apt-get install librealsense2-dev`  
  `sudo apt-get install librealsense2-dbg`  
  With `dev` package installed, you can compile an application with **librealsense** using `g++ -std=c++11 filename.cpp -lrealsense2` or an IDE of your choice.

Reconnect the Intel RealSense depth camera and run: `realsense-viewer` to verify the installation.

Verify that the kernel is updated :    
`modinfo uvcvideo | grep "version:"` should include `realsense` string

## Step 2: [Install Intel® RealSense™ ROS from Sources](https://github.com/IntelRealSense/realsense-ros/tree/ros1-legacy)

```
echo "source ~/camera/devel/setup.bash" >> ~/.bashrc
```

## Camera Calibration

```bash
$ roslaunch camera_calibration camera_calibration.launch
$ rosrun camera_calibration cameracalibrator.py --size 7x6 --square 0.01 image:=/camera/rgb/image_raw camera:=/camera/rgb # 新建终端并不要source
```

