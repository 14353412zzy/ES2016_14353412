#Ubuntu install of ROS Jade
##1 Installation
###1.1 Configure your Ubuntu repositories
![enter image description here](https://raw.githubusercontent.com/14353412zzy/ES2016_14353412/master/pictures/repositories.png)
###1.2 Setup your sources.lis
	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'	
###1.3 Set up your keys
	sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
###1.4 Installation
#####依次执行以下命令
	sudo apt-get update
	sudo apt-get install ros-jade-desktop-full
	sudo apt-get install ros-jade-desktop
	sudo apt-get install ros-jade-ros-base
	sudo apt-get install ros-jade-PACKAGE
	sudo apt-get install ros-jade-slam-gmapping
	apt-cache search ros-jade
###1.5 Initialize rosdep
	sudo rosdep init
	rosdep update
###1.6 Environment setup
	echo "source /opt/ros/jade/setup.bash" >> ~/.bashrc
	source ~/.bashrc
	source /opt/ros/jade/setup.bash
###1.7 Getting rosinstall
	sudo apt-get install python-rosinstall
##2 Tutorials
###2.1 Obtain source code of the installed packages
	apt-get source ros-jade-laser-pipeline

#cartographer
####0.安装所有依赖项
	sudo apt-get install -y google-mock libboost-all-dev  libeigen3-dev libgflags-dev libgoogle-glog-dev liblua5.2-dev libprotobuf-dev  libsuitesparse-dev libwebp-dev ninja-build protobuf-compiler python-sphinx  ros-indigo-tf2-eigen libatlas-base-dev libsuitesparse-dev liblapack-dev
####1.安装ceres solver
	git clone https://github.com/hitcm/ceres-solver-1.11.0.git
	cd ceres-solver-1.11.0/build //(build文件夹需要手动新建)
	cmake ..
	make
	sudo make install
####2.安装 cartographer
	git clone https://github.com/hitcm/cartographer.git
	cd cartographer/build
	cmake .. -G Ninja
	ninja
	ninja test
	sudo ninja install
####3.安装cartographer_ros
#####新建catkin_ws\src文件夹，并进入
	git clone https://github.com/hitcm/cartographer_ros.git
#####这样clone来的会缺少"tf2_eigen"文件，所以需要补上；
	// Install wstool and rosdep.
	sudo apt-get update
	sudo apt-get install -y python-wstool python-rosdep ninja-build
	cd catkin_ws
	wstool init src
	// Merge the cartographer_ros.rosinstall file and fetch code for dependencies.
	wstool merge -t src https://raw.githubusercontent.com/googlecartographer/cartographer_ros/master/cartographer_ros.rosinstall
	wstool update -t src
	
	// Install deb dependencies.
	rosdep init
	rosdep update
	rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y
	
	//Build and install.//(需要翻墙)
	catkin_make_isolated --install --use-ninja
	source install_isolated/setup.bash

####构建图像：
	// Download the 2D backpack example bag.
	wget -P ~/Downloads https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag

	// Launch the 2D backpack demo.
	roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
	
##结果截图： 
![enter image description here](https://raw.githubusercontent.com/14353412zzy/ES2016_14353412/master/pictures/Cartographer%20.png)