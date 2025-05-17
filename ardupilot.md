
<h1 align="center"><b> 🛩 ArduPilot with ROS 2 Humble Installation Guide </b></h1>

> This guide will set up:

* ArduPilot (latest from source)
* Micro-XRCE DDS

---

## 🧱 1. Install Dependencies

```bash
sudo apt-get update
sudo apt-get install git
sudo apt-get install gitk git-gui
```

---

## 🛠 2. Clone and Build ArduPilot

### 📁 Clone ArduPilot

```bash
cd ~
git clone https://github.com/ArduPilot/ardupilot.git
cd ardupilot
git submodule update --init --recursive
```

### ⚙️ Install ArduPilot Dependencies

```bash
Tools/environment_install/install-prereqs-ubuntu.sh -y
. ~/.profile
```

---

### 📝 Add this to .bashrc file

```bash
export PATH=$PATH:$HOME/ardupilot/Tools/autotest
export PATH=/usr/lib/ccache:$PATH
```

Now, Reload the PATH

```bash
. ~/.bashrc
```

---

## 🛰 3. Installation of Communication protocol Micro-XRCE 

> MAVROS2 is used for communication via MAVLink.

### 📦 Clone the required repositories using vcs and a ros2.repos files:

```bash
mkdir -p ~/ardu_ws/src
cd ~/ardu_ws
vcs import --recursive --input  https://raw.githubusercontent.com/ArduPilot/ardupilot/master/Tools/ros2/ros2.repos src
```

### 🌐 Update all dependencies:

```bash
cd ~/ardu_ws
sudo apt update
rosdep update
source /opt/ros/humble/setup.bash
rosdep install --from-paths src --ignore-src -r -y
```

---

### 🌐 Installing the MicroXRCEDDSGen build dependency:

```bash
sudo apt install default-jre
cd ~/ardu_ws
git clone --recurse-submodules https://github.com/ardupilot/Micro-XRCE-DDS-Gen.git
cd Micro-XRCE-DDS-Gen
./gradlew assemble
echo "export PATH=\$PATH:$PWD/scripts" >> ~/.bashrc
```

---

### 🌐 Test the MicroXRCEDDSGen Agent:

```bash
source ~/.bashrc
microxrceddsgen -help
```
The Output should display this,
```bash
# microxrceddsgen usage:
#     microxrceddsgen [options] <file> [<file> ...]
#     where the options are:
#             -help: shows this help
#             -version: shows the current version of eProsima Micro XRCE-DDS Gen.
#             -example: Generates an example.
#             -replace: replaces existing generated files.
#             -ppDisable: disables the preprocessor.
#             -ppPath: specifies the preprocessor path.
#             -I <path>: add directory to preprocessor include paths.
#             -d <path>: sets an output directory for generated files.
#             -t <temp dir>: sets a specific directory as a temporary directory.
#             -cs: IDL grammar apply case sensitive matching.
#     and the supported input files are:
#     * IDL files.
```

---

### 🌐 Building the Workspace

```bash
cd ~/ardu_ws
colcon build --packages-up-to ardupilot_dds_tests
```

---

## 🔁 4. Run ArduPilot SITL + MicroXRCE-DDS

### 🚁 Launch ArduPilot SITL

```bash
cd ~/ardupilot/
export PATH=$PATH:~/ardu_ws/src/ardupilot/Tools/autotest
sim_vehicle.py -v ArduCopter --console -DG --enable-dds
```

This starts SITL on UDP ports.

---

### 🔌 Run DDS agent:

Open another terminal:

```bash
source /opt/ros/humble/setup.bash
cd ~/ardu_ws/
colcon build --packages-up-to ardupilot_sitl
source install/setup.bash
ros2 launch ardupilot_sitl sitl_dds_udp.launch.py transport:=udp4 synthetic_clock:=True wipe:=False model:=quad speedup:=1 slave:=0 instance:=0 defaults:=$(ros2 pkg prefix ardupilot_sitl)/share/ardupilot_sitl/config/default_params/copter.parm,$(ros2 pkg prefix ardupilot_sitl)/share/ardupilot_sitl/config/default_params/dds_udp.parm sim_address:=127.0.0.1 master:=tcp:127.0.0.1:5760 sitl:=127.0.0.1:5501
```

Check the Active ROS2 Nodes and Services:

```bash
source ~/ardu_ws/install/setup.bash
# See the node appear in the ROS graph
ros2 node list
# See which topics are exposed by the node
ros2 node info /ap
# Echo a topic published from ArduPilot
ros2 topic echo /ap/geopose/filtered
```


## 🧠 Add GCS (QGroundControl)

Install QGroundControl for visual monitoring:

1. On the command prompt enter:

```bash
sudo usermod -a -G dialout $USER
sudo apt-get remove modemmanager -y
sudo apt install gstreamer1.0-plugins-bad gstreamer1.0-libav gstreamer1.0-gl -y
sudo apt install libfuse2 -y
sudo apt install libxcb-xinerama0 libxkbcommon-x11-0 libxcb-cursor-dev -y
```

2. **Download the AppImage in Home Directory: [QGCAppImage](https://d176tv9ibo4jno.cloudfront.net/latest/QGroundControl.AppImage)**

3. Install (and run) using the terminal commands:

```bash
chmod +x ./QGroundControl.AppImage
```

5. Now to Launch the GCS, run the following commands:

```bash
cd ~/
./QGroundControl.AppImage
```

---

## 📦 References

* [micro-ROS documentation](https://micro.ros.org)
* [ArduPilot Dev Docs](https://ardupilot.org/dev/)
* [Micro XRCE-DDS](https://github.com/eProsima/Micro-XRCE-DDS)
* [ros2/micro\_ros\_setup](https://github.com/micro-ROS/micro_ros_setup)

---

# Next: [Task 2.2](https://github.com/ShaneshrajeK/Aero_Modelling_Club_Summer_Camp_2025/blob/main/Week_2/task2.md)
