FROM ros:melodic

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
# dependencies of https://github.com/project-omicron/gazebo_simulation follow
    ros-melodic-gazebo-ros \
    ros-melodic-teleop-twist-keyboard \
    ros-melodic-joint-state-publisher \
    ros-melodic-dynamic-robot-state-publisher \
    ros-melodic-xacro \
    ros-melodic-rviz \
    ros-melodic-compressed-image-transport \
    ros-melodic-theora-image-transport \
    ros-melodic-camera-info-manager \
 && rm -rf /var/lib/apt/lists/*
