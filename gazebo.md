
<h1 align="center"> 🧱 Gazebo Harmonic Installation Guide </h1>

Gazebo Harmonic is part of the **modern Gazebo family (gz-sim)** and is **not installed** via traditional `gazebo11`. It uses the new modular `gz-*` toolchain.

---

## ✅ Step-by-Step Installation

### 📌 Step 1: Add the OSRF Apt Repository

```bash
sudo apt update
sudo apt install curl gnupg lsb-release -y
```

```bash
sudo curl https://packages.osrfoundation.org/gazebo.gpg --output /usr/share/keyrings/pkgs-osrf-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/pkgs-osrf-archive-keyring.gpg] http://packages.osrfoundation.org/gazebo/ubuntu-stable $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/gazebo-stable.list > /dev/null

```

---

### 📌 Step 2: Install Gazebo Harmonic

```bash
sudo apt update
sudo apt install gz-harmonic -y
```

---

### 📌 Step 3: Verify Installation

Run:

```bash
gz sim
```

You should see the Gazebo Harmonic simulator GUI launch.

---

## ✅ Optional: Install Full Toolchain

To get all useful tools:

```bash
sudo apt install gz-harmonic-all -y
```

This includes:

* `gz sim`: Main simulation tool
* `gz fuel`: Asset browser
* `gz topic`, `gz service`: CLI tools
* `gz sdf`, `gz model`, etc.

---

## 🧪 Test Example Simulation

```bash
gz sim shapes.sdf
```

(You can find sample worlds in `/usr/share/gz/sim/worlds/`)

---

## 📌 Important:

* **ROS 2 Integration**: Gazebo Harmonic is **not natively integrated** with ROS 2 Humble. For that, use the **`ros_gz` bridge**:
  [https://github.com/gazebosim/ros\_gz](https://github.com/gazebosim/ros_gz)

* If you want to use Harmonic with ROS 2, install:

```bash
sudo apt install ros-humble-ros-gz
```

---

# Next: [ArduPilot Installation](https://github.com/ShaneshrajeK/Aero_Modelling_Club_Summer_Camp_2025/blob/main/Week_2/ardupilot.md)
