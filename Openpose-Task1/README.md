
# OpenPose Doc - Installation

## _For Windows_ 

Step 1 - Install visual studio 2017 enterprise <br/>
For openpose select all c++ options and windows 8.1 SDK.

Step 2 -Install CUDA

Step 3 - Download cudnn <br/>
https://developer.nvidia.com/rdp/cudnn-archive 

A list of links will appear out of which you are to select the link for the version of CUDA and cudnn available to you. You can check these versions by:
 <br />
  <br />
For cudnn: Go to My PC --> Downloads --> cudnn 10.0 windows10x64x7.5.0.56 --> cuda <br />
For CUDA: Go to My PC --> ( C ) --> Program Files --> NVIDIA GPU Computing Toolkits --> CUDA --> v 10.0 <br />

Step 4 - Clone the OpenPose repository.
```sh
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
cd openpose/
git submodule update --init --recursive --remote
```

Step 5- CMake Configuration
1) Go to the OpenPose folder and open CMake-GUI from it. On Windows, double click on CMake-gui.
```sh
cd {OpenPose_folder}
mkdir build/
cd build/
cmake-gui ..
```

2) Select the Openpose directory as project source directory. (eg. build) 

3) Press the configure button, select 64-bit Visual Studio version and press finish. e.g., Visual Studio 16 2019, and then you must manually choose x64 for the Optional platform for generator.

4) Enabling Python (optional step, only apply it if you plan to use the Python API) --> Enable the BUILD_PYTHON flag and click Configure again.

5) Set the GPU_MODE flag to the proper value and click Configure again:  <br />
i) If your machine has an Nvidia GPU, you should most probably not modify this flag and skip this step. <br />
ii) If your machine does not have any GPU, set the GPU_MODE flag to CPU_ONLY. <br />

6) If this step is successfull, then configuring done text will get appear in the last line. Otherwise, some red text will appear in the same bottom box.

7) Press the Generate button. You can now close CMake.

8) Open Visual Studio 2019 after we press the ‘Open Project’ button.

9) First, we need to alter from Debug mode to Release mode. We then need to go to the “Build” menu, and press “Build Solution” . Wait until it is all done, Once everything is sucessfull completed that means we have successfully installed openpose on your computer.

Step 6 - Create folders in examples folder -->    <br />
```sh
|-- outputdata/data
      |-- /images --> to store the output of openpose image. 
      |-- /keypoints --> to store the generate keypoints. 
      |-- /video --> to store the generated openpose video.
```

Step 7 - Now, you can run a demo using the following code:
```sh
C:\Users\223066622\Documents\Project Arbeit\project\openpose\build\x64\Release>OpenPoseDemo.exe --face --hand --keypoint_scale 3 --frame_step 3 --video "..\..\..\examples\media\se.flv" --write_json ..\..\..\examples\output\data\keypoints --display 0 --write_video ..\..\..\examples\output\data\video\openpose.avi --write_images ..\..\..\examples\output\data\images
```

## _For Ubuntu_

Step 1 - Make sure anaconda is uninstalled from your system
```sh
rm -rf ~/anaconda3/
```

Step 2 - Check your CUDA version using
```sh
nvcc --version
```
If CUDA is not installed, install nvidia toolkit using 

```sh
sudo apt-get install nvidia-cuda-toolkit
```
and reboot.

Step 3 -  Download cuDNN tgz file with version mentioned in system configuration, unzip it and run

Download cudnn-8.0-linux-x64-v5.1 file from https://github.com/leestott/Azure-GPU-Setup/issues/1 and unzip the file.
```sh
cp -r cudnn-8.0-linux-x64-v5.1 /usr/local
```

Step 4 - Install opencv
```sh
sudo apt install libopencv-dev python3-opencv
```

Step 5 - Install and configure gcc version
```sh
sudo apt update
sudo apt install build-essential
sudo apt-get install manpages-dev
gcc --version
```

Step 6- Install cmake , wget zip file of cmake-3.15.6.tar.gz
```sh
wget https://github.com/Kitware/CMake/releases/download/v3.15.6/cmake-3.15.6.tar.gz 
tar -zxvf cmake-3.15.6.tar.gz 
cd cmake-3.15.6 
```

Step 7 - Now, clone openpose from the github
```sh
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
cd openpose/
sudo bash ./scripts/ubuntu/install_deps.sh
sudo apt install caffe-cuda
```

Step 8 -  Manually clone Caffe and Pybind11 to 3rdparty folder
```sh
cd openpose/3rdparty/
git clone https://github.com/CMU-Perceptual-Computing-Lab/caffe.git
git clone https://github.com/pybind/pybind11
```

Step 9 - Configure and make the build for OpenPose
```sh
cd {OpenPose_folder}
mkdir build/
cd build/
cmake-gui ..
```
select the configs you want. Make sure to check build caffe, use cuDNN and openCV. Hit ‘Configure’ and then ‘Generate’. Then close cmake.

Step 10 - Build OpenPose
```sh
cd build/
make -j5
```

Step 11 -  Now, you can run a demo using the following code:
```sh
cd ..
./build/examples/openpose/openpose.bin --face --hand --keypoint_scale 3 --frame_step 3 --video "..\..\..\examples\media\se.flv" --write_json ..\..\..\examples\output\data\keypoints --display 0 --write_video ..\..\..\examples\output\data\video\openpose.avi --write_images ..\..\..\examples\output\data\images
```


