FROM ros:melodic

ARG DEBIAN_FRONTEND noninteractive
WORKDIR /root/catkin_ws/src

ENV NVIDIA_VISIBLE_DEVICES ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics

RUN apt-get update && apt-get install -y --no-install-recommends \
	wget \
	vim \
	build-essential \
	libgoogle-glog-dev \
	automake \
	libtool \
	m4 \
	rsync \
	automake \
        python-wstool \
	python-catkin-tools \
	protobuf-compiler \
	autoconf \
	libomp-dev \
        libmetis-dev \
	mesa-utils \
	x11-apps \
        ros-melodic-pcl-ros \
	ros-melodic-cmake-modules \
	ros-melodic-eigen-conversions \
	ros-melodic-tf-conversions \
	ros-melodic-rviz \
	ros-melodic-cv-bridge \
 	&& apt-get clean && rm -rf /var/lib/apt/lists/*

RUN /bin/bash -c '. /opt/ros/melodic/setup.bash; catkin_init_workspace'
RUN cd .. && catkin init \
	&& catkin config --extend /opt/ros/melodic\
	&& catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release \
	&& catkin config --merge-devel

COPY . /root/catkin_ws/src/voxblox

RUN wstool init . ./voxblox/voxblox_https.rosinstall
RUN wstool update

RUN /bin/bash -c '. /opt/ros/melodic/setup.bash; catkin build voxblox_ros'
RUN sed -i "6i source \"/root/catkin_ws/devel/setup.bash\"" /ros_entrypoint.sh

ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["bash"]
