### Cartographer
0.安装所有依赖项
``` sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev``` ![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/9.png?raw=true)

1 首先安装ceres solver，选择的版本是1.11,路径随意

```git clone https://github.com/hitcm/ceres-solver-1.11.0.git```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/2.png?raw=true)
首先新建在ceres-solver-1.11.0里面新建一个build文件夹然后进入build文件夹：
```cd ceres-solver-1.11.0/build```
```cmake ..```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/3.png?raw=true)
```make```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/4.png?raw=true)
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/5.png?raw=true)
```sudo make install```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/6.png?raw=true)
<br>
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/7.png?raw=true)


2然后安装 cartographer,路径随意
```git clone https://github.com/hitcm/cartographer.git```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/8.png?raw=true)
```cd cartographer/build```
```cmake .. -G Ninja```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/9.png?raw=true)

```ninja```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/10.png?raw=true)

```ninja test```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/11.png?raw=true)

![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/12.png?raw=true)

```sudo ninja install```


3安装cartographer_ros
新建carkin_ws/src文件夹，然后下载到catkin_ws下面的src文件夹下面
```git clone https://github.com/hitcm/cartographer_ros.git```
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/14.png?raw=true)
然后到catkin_ws下面运行catkin_make即可。
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/15.png?raw=true)
这样会有错误：cmake error。
然后输入下面的指令：
```//install wstool and rosdep.```
```sudo apt-get update```
```sudo apt-get install -y python-wstool python-rosdep ninja-build```

```Create a new workspace in 'catkin_ws'.```
```mkdir catkin_ws```
```cd catkin_ws```
```wstool init src```

```// Merge the cartographer_ros.rosinstall file and fetch code for dependencies.```
```wstool merge -t src https://raw.githubusercontent.com/googlecartographer/cartographer_ros/master/cartographer_ros.rosinstall```
```wstool update -t src```

```// Install deb dependencies.```
```rosdep init```
```rosdep update```
```rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y ```
再运行```catkin_make```命令
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/16.png?raw=true)

4.下载数据
下载2d数据包：
```wget -P ~/Downloads https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag```
运行数据包：
```roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag```
第一次跑到这里一般会有这个错误：
> [demo_backpack_2d.launch] is neither a launch file in package
[cartographer_ros] nor is [cartographer_ros] a launch file name The traceback
for the exception was written to the log file

这种错误的主要原因是ros的catkin_ws配置问题，可以运行 ```rospack profile``` 试试。
接下来应该还有可能说一个连接不上server的问题，解决办法如下：
```cd```
```gedit ~/.bashrc```
最后三行加上
```export```
```ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:/home/siat/ccny/ccny_vision:/home/siat/catkin_ws/src```
```export ROS_HOSTNAME=localhost```
```export ROS_MASTER_URI=http://localhost:11311```
最终结果：
![enter image description here](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/Cartographer/17.png?raw=true)
