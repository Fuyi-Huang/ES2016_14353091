### ROS Installation 
1. Configure your Ubuntu repositories![sofeware.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/Software%20Sources.png?raw=true)

2. Setup your sources.list![1.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/1.png?raw=true)

3. Set up your keys
![2.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/2.png?raw=true)

4. Installation 
First, make sure your Debian package index is up-to-date: 
 ``` sudo apt-get update ```![3.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/3.png?raw=true)
Desktop-Full Install : ROS, rqt, rviz, robot-generic libraries, 2D/3D simulators, navigation and 2D/3D perception 
 ``` sudo apt-get install ros-jade-desktop-full```![4.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/4.png?raw=true)
ROS-Base: (Bare Bones) ROS package, build, and communication libraries. No GUI tools. ``` sudo apt-get install ros-jade-ros-base```
![5.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/5.png?raw=true)


5. Initialize rosdep
 ``` sudo rosdep init  ``` 
 ``` rosdep update``` ![6.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/6.png?raw=true)  <br/> ![7.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/7.png?raw=true)

6. Environment setup
 ``` echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc```
 ``` source ~/.bashrc``` ![8.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/8.png?raw=true)

7. Getting rosinstall
``` sudo apt-get install python-rosinstall```![9.png](https://github.com/Fuyi-Huang/ES2016_14353091/blob/master/images/ROS/9.png?raw=true)
