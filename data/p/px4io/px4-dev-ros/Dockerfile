#  
# PX4 ROS development environment  
#  
  
FROM px4io/px4-dev-simulation  
MAINTAINER Daniel Agar <daniel@agar.ca>  
  
RUN apt-key adv \--keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key
421C365BD9FF1F717815A3895523BAEEB01FA116 \  
&& sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" >
/etc/apt/sources.list.d/ros-latest.list' \  
&& sh -c 'echo "deb http://packages.ros.org/ros-shadow-fixed/ubuntu/ xenial
main" > /etc/apt/sources.list.d/ros-shadow.list' \  
&& apt-get update \  
&& apt-get -y \--quiet --no-install-recommends install \  
geographiclib-tools \  
libgeographic-dev \  
python-tk \  
python-catkin-tools \  
ros-kinetic-gazebo-ros-pkgs \  
ros-kinetic-mavlink \  
ros-kinetic-mavros \  
ros-kinetic-mavros-extras \  
ros-kinetic-ros-base \  
&& geographiclib-get-geoids egm96-5 \  
&& apt-get -y autoremove \  
&& apt-get clean autoclean \  
# pip  
&& pip install matplotlib numpy px4tools pymavlink \  
&& rm -rf /var/lib/apt/lists/{apt,dpkg,cache,log} /tmp/* /var/tmp/*  
  
RUN rosdep init && rosdep update  

