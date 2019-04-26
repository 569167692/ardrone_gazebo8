# ardrone_gazebo8
## 基于Gazebo仿真平台（Gazebo8版本）和Parrot Ardrone2.0飞行器，搭建所需要的仿真环境。  
  
这是自己随便搭建的一个仿真环境，并进行ardrone的自主控制算法验证 于2019年4月27日 0:02添加

## 操作系统：ubuntu16.04  
## ROS：kinetic  
## Gazebo：8.6

## 安装步骤：  
### 1.安装Gazbeo8环境  
    (1)添加sources.list  
    sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
    (2)添加key
    wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
    (3)更新软件
    sudo apt-get update
    (4)安装gazebo8
    sudo apt-get install gazebo8
    sudo apt-get install libgazebo8-dev
### 2.安装ros kinetic（不安装full版）  
    (1)添加sources.list
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    (2)添加key
    sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
    (3)更新软件
    sudo apt-get update
    (4)安装ros-kinetic-desktop
    sudo apt-get install ros-kinetic-desktop
    (5)初始化rosdep
    sudo rosdep init
    rosdep update
    (6)环境变量配置
    echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    (7)安装rosinstall
    sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential  
### 3.安装相关ros包 和其他python库
    (1)安装ros包
    sudo apt-get install ros-kinetic-ardrone-autonomy
    sudo apt-get install ros-kinetic-gazebo8-msgs
    sudo apt-get install ros-kinetic-gazebo8-ros-control
    sudo apt-get install ros-kinetic-gazebo8-plugins
    sudo apt-get install ros-kinetic-gazebo8-ros-pkgs
    sudo apt-get install ros-kinetic-gazebo8-ros
    sudo apt-get install ros-kinetic-image-view  
    
    (2)安装键盘控制程序所需python库
    sudo apt-get install python-pyside
### 4.搭建仿真环境
    (1)创建工作空间
    mkdir -p ~/catkin_ws/src
    cd  ~/catkin_ws
    catkin_make
    source devel/setup.bash
    
    (2)下载ardrone_autonomy包到 ~/catkin_ws/src目录下，ardrone_autonomy是ardrone无人机飞行所需要的驱动包
    
    (3)下载ardrone_simulator_gazebo7包到 ~/catkin_ws/src目录下，ardrone_simulator_gazebo7是ardrone无人机所处的仿真世界环境
    
    (4)下载ardrone_tutorials包到 ~/catkin_ws/src目录下，ardrone_tutorials是ardrone的键盘控制程序
    
    (5)编译环境
    catkin_make
    
    (6)配置环境(~/.bashrc文件)
    在~/.bashrc文件末尾添加如下两行代码
    source ~/catkin_ws/devel/setup.bash
    
    配置gazebo model路径,我的pwd为"/home/cug/catkin_ws/src/ardrone_simulator_gazebo7/cvg_sim_gazebo/models",根据自己的路径相应修改
    export GAZEBO_MODEL_PATH=pwd
    
    (7)Source 环境
    source ~/.bashrc
    source devel/setup.bash  
### 5.运行仿真环境
    (1)启动launch文件，打开gazebo仿真世界模型
    cd catkin_ws
    source devel/setup.bash
    roslaunch cvg_sim_gazebo ardrone_testworld.launch
    
    (2)运行键盘控制程序
    注：若是第一次运行键盘控制程序，需要先将py程序变为可执行文件，只要执行过此步骤，以后都不需要再直行具体操作如下
    cd ~/catkin_ws/src/ardrone_tutorials/src
    chmod +x *.py
    
    运行键盘控制程序
    cd catkin_ws
    source devel/setup.bash
    rosrun ardrone_tutorials keyboard_controller.py


    
