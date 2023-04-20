# slam_subt
how to run subt:
./subt/docker/run.bash osrf/subt-virtual-testbed:latest  circuit:=cave  cave_circuit.ign    worldName:=simple_cave_01    robotName1:=X1 robotConfig1:=EXPLORER_X1_SENSOR_CONFIG_1

sudo docker run -it -d --rm -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v $HOME/.Xauthority/:/root/.Xauthority:rw -v $PWD:/home/ws --privileged -e DISPLAY=$DISPLAY --network=host {IMAGE_PID}  /bin/bash

docker run -it  -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v $HOME/.Xauthority/:/root/.Xauthority:rw -v $PWD:/home/ws --privileged -e DISPLAY=$DISPLAY --network=host 6a74c5a63767  /bin/bash

docker exec -it `docker ps --filter ancestor=osrf/subt-virtual-testbed --format {{.ID}}` /bin/bash

sudo apt-get update && sudo apt-get install ros-melodic-teleop-twist-keyboard
rosrun teleop_twist_keyboard teleop_twist_keyboard.py /cmd_vel:=/X1/cmd_vel
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 X2/base_link X2/odom 1
rosrun tf tf_echo /X1/base_link/front_laser /X1/base_link/imu_sensor
roslaunch imu_filter_madgwick imu_filter_madgwick.launch
roslaunch lio_sam run.launch
