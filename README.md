##
目前这个项目包含2025Robocup无人机识别与快递运输赛的任务代码以及2024年电子设计大赛无人机赛道的相关代码。
后续可能会补充25年和26年电子设计大赛无人机题的代码（取决于今年成绩了）
## 项目结构
```sh
tutorial
│
├── 2024NUEDC/src                
│   ├──square_demo
│   ├──vins_to_mavros
│   └──vision_to_mavros
│
├── catkin_ws/src
│   ├──quadrotor_msgs
│   └──tracking_controller
│
└── Robocup_2025/src
    ├──mission_node  
    ├──quadrotor_msgs
    └──vins_to_mavros           
```

# **引言**
感谢飞控组所有前辈做出的贡献，也希望飞控组越来越好

这里附上前组长们总结的学习路线
1.赵虚左老师ROS入门课程。看完话题通信服务通
行就可以实现简单的ROS任务了，剩下的内容遇
到实际问题在反过头来看。
【【Autolabor初级教程】ROS机器人入门】
https://www.bilibili.com/video/BV1Ci4y1L7ZZ/?
share_source=copy_web&vd_source=e397b600
513156b0a277ca7978233795
2.机器人工匠阿杰的ROS入门课程，学习ROS传感
器，导航的相关算法和仿真实现。
【机器人操作系统 ROS 快速入门教程】
https://www.bilibili.com/video/BV1BP4y1o7pw/?
share_source=copy_web&vd_source=e397b600
513156b0a277ca7978233795
3.路径规划算法Ego-Planner的实机部署
【【完结】从0制作自主空中机器人 | 开源 | 浙江
大学Fast-Lab】
https://www.bilibili.com/video/BV1WZ4y167me/?
share_source=copy_web&vd_source=e397b600
513156b0a277ca7978233795
4.无人机仿真环境XTDrone搭建
https://www.yuque.com/xtdrone/manual_cn/bas
ic_config_13

下面的内容也很推荐
1.ROS无人机基础知识
【【浙江大学】浙大博导带你从0制作无人机】
https://www.bilibili.com/video/BV1cM4y1Z7Zs/?
share_source=copy_web&vd_source=e397b600
513156b0a277ca7978233795
2.双系统安装（如有需要）
【Windows 10 和 Ubuntu 双系统的安装和卸
载】
https://www.bilibili.com/video/BV1554y1n7zv/?
share_source=copy_web&vd_source=e397b600
513156b0a277ca7978233795

视觉传统OpenCV没有必要专门学习，找几个项目复
现一下，了解基本实现即可。保证能够在需要
OpenCV时依靠AI实现功能。
色块追踪项目
https://github.com/1zlab/1ZLAB_Color_Block_Finder.
git
yolov5，这个需要通过实际的项目学习



## 基础知识
### Linux
无人机的相关代码都是在Linux系统上实现的，所以Linux操作系统是机器人工程师的基本功。这一部分直接去B站找相关的教学视频粗略学习即可
### ROS
ROS是一个做机器人必不可少的元操作系统，他一般在Linux系统下使用，这里推荐B站赵虚左老师的课程
[链接](https://www.bilibili.com/video/BV1Ci4y1L7ZZ/?share_source=copy_web&vd_source=e397b600513156b0a277ca7978233795)

在视频学习中你将会学习到虚拟机，ubuntu系统和ROS的基础操作。
## 从无人机仿真开始
无人机是一个极其烧钱的东西，作者用来参加电赛的无人机制作成本将近1万元，加上平时炸机的损耗，费用是惊人的。大多数人止步于此，但是我们可以先从仿真做起，等领略过无人机的魅力后再组装无人机不迟。
### 无人机仿真平台
仿真平台我推荐肖昆老师的XTDrone
```
https://gitee.com/robin_shaun/XTDrone.git
```
## 无人机组装
初学者的第一架无人机我推荐浙江大学高飞老师的fast-drone-250。理由是小飞机的安全性比较高而且用到的传感器也比较便宜，而且有完整的purchase list和相关的组装视频，学起来简单易上手。也为之后学习路径规划做铺垫。


这是相关视频

[【【完结】从0制作自主空中机器人 | 开源 | 浙江大学Fast-Lab】 ](https://www.bilibili.com/video/BV1WZ4y167me/?share_source=copy_web&vd_source=e397b600513156b0a277ca7978233795)

这是项目的仓库

```
https://github.com/ZJU-FAST-Lab/Fast-Drone-250.git
```

无人机的相关基础知识

[【无人机教程】从零开始学习无人机原理及组装】 ]( https://www.bilibili.com/video/BV1bE411u7nv/?share_source=copy_web)

无人机在室内往往接收不到GPS信号，一般使用激光slam算法，或者视觉slam算法

我们的飞机搭配的是mid360激光雷达与Fast-lio算法

```
https://github.com/hku-mars/FAST_LIO.git
```
# **2025Robocup比赛代码配置**
## 安装Mavros
```
sudo apt-get install ros-noetic-mavros
cd /opt/ros/noetic/lib/mavros
sudo ./install_geographiclib_datasets.sh
```
其中的noetic要换成相应的ROS版本。
## 配置SLAM: Fast-lio2
官方仓库
```
https://github.com/hku-mars/FAST_LIO.git
```
配置Fast-lio2还需要额外配置Mid360配套的SDK和驱动，我推荐上CSDN跟着教程配置。多个教程互补着看

[CSDN教程1 ]( https://blog.csdn.net/m0_55117804/article/details/142644882?fromshare=blogdetail&sharetype=blogdetail&sharerId=142644882&sharerefer=PC&sharesource=simonluxing&sharefrom=from_link)

[CSDN教程2 ]( https://lanxzheng.blog.csdn.net/article/details/132408005?fromshare=blogdetail&sharetype=blogdetail&sharerId=132408005&sharerefer=PC&sharesource=simonluxing&sharefrom=from_link)

## 配置Ego-planner
 推荐东北大学REAL实验室的教程
```
https://github.com/NEU-REAL/REAL_DRONE_400.git
```

## 配置我们的控制器和任务代码

```
git clone https://github.com/luxting/CSU-EK-Drone-Tutorial.git
```
把build和devel文件夹删了然后
```
catkin_make
```
