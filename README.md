# Turtlebot4_navigation from point A to point B
In my midterm exam project, the goal is to move to point A and activate the buzzer once, then move the robot to point B and activate the buzzer twice.
************************************************
# How to Build

#### Create folder workspace
```
mkdir kelompok4a_uts/src
cd kelompok4a_uts/src
```
disini membuat folder workspace dengan struktur standar ROS2,dan masuk ke folder tempat package yang dibuat, folder tersebut masuk ke dalam src
#### Create package and dependencies
```
source /opt/ros/jazzy/setup.bash
ros2 pkg create --build-type ament_cmake --node-name navkel4a navkel4a --dependencies rclcpp nav2_msgs rclcpp_action tf2
```
tahap ini mengaktifkan environment ROS2 agar dikenali lalu membuat package baru didalam src bernama **navkel4a** dengan jenis kompilasi ROS2 dengan file node utama bernama **navkel4a.cpp**

Pada dependecies library yang digunakan rclcpp untuk menulis node C++
#### build the package
```
colcon build
```
**colcon build** melakukan kompilasi semua package dalam workspace untuk menghasilkan folder install/ yang berisi node ROS2
************************************************
# Connect From PC to Robot Turtlebot4

Connet wired via manual setting **Ip addres 192.168.185.6**, gateway **255.255.255.0**, and Netmask **192.168.185.3** and open terminal type this :
```
ssh ubuntu@192.168.185.3
```
pada tahap ini untuk mengontrol robot dari pc melalui jaringan kabel dan turtlebot4 berjalan di sistem ubuntu
**********************************************
# Mapping

#### SLAM launch
```
ros2 launch turtlebot4_navigation slam.launch.py
```
disini menjalankan node SLAM untuk membuat map dan mengaktifkan sensor LIDAR dan package navigasi dan robot dapat digerakkan.
#### Running Rviz
because i`am using ubuntu24 use jazzy type this:
```
ros2 launch turtlebot4_viz view_navigation.launch.py
```
disini menjalankan Rviz untuk melihat visualisasi seperti peta yang sedang dibentuk, posisi robot, data liDAR dan transformasi frame.
************************************************
# Running Nav2 (Navigasi)

#### Navigation launch
```
ros2 launch nav_kel4a run_nav.launch.py
```
Menjalankan konfigurasi navigasi yang disiapkan dalam package **nav_kel4a**
#### Localization launch
```
ros2 launch turtlebot4_navigation localization.launch.py map:=kelompok4A_uts/src/nav_kel4a/maps/kel4a.yaml
```
mengaktifkan AMCL untuk lokalisasi untuk menentukan posisi robot pada map sekaligus mengaktifkan Nav2 dan menunjukan peta yang sebelumnya dibuat saat maaping
#### Running Rviz
because i`am using ubuntu24 use jazzy type this:
```
ros2 launch turtlebot4_viz view_navigation.launch.py
```
menampilkan posisi robot setelah localization aktif
#### Running call Program 
```
ros2 run nav_kel4a nav_kel4a
```
Langkah terakhir menjalankan node C++ yang telah dibuat dimana node program berisi kirim goal ke point A dan buzzer berbunyi 1x setelah itu pergi ke point B dan akan berbunyi 2x

#### Video Penjelasan dan video demonstrasi pada robot
👉 [Video Penjelasan](https://youtu.be/vMAmRzkJztY)

👉 [Video demonstrasi Robot](https://youtu.be/YAc0uz2JfPw)

