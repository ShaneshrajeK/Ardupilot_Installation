<h1 align="center">ROS2: Humble Hawksbill Installation</h1>

---

## ✅ Prerequisites

1. **Operating System**: Ubuntu 22.04 (64-bit)
2. **User Privileges**: Root/sudo access

---

## 🧩 Step 1: Set Locale

```bash
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

---

## 🔐 Step 2: Add ROS 2 GPG Key

```bash
sudo apt install curl gnupg lsb-release
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo gpg --dearmor -o /usr/share/keyrings/ros-archive-keyring.gpg
```

---

## 📦 Step 3: Add ROS 2 Repository

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] \
https://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

## 🔄 Step 4: Update Package Index

```bash
sudo apt update
```

---

## 🧰 Step 5: Install ROS 2 Humble



```bash
sudo apt install ros-humble-desktop
```


### Development Tools

```bash
sudo apt install ros-dev-tools
```

---

## 🛠 Step 6: Environment Setup

### Add to `~/.bashrc`:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

> If using **zsh**:

```bash
echo "source /opt/ros/humble/setup.zsh" >> ~/.zshrc
source ~/.zshrc
```

---

## 🧪 Step 7: Test the Installation

```bash
ros2 run demo_nodes_cpp talker
```

In a new terminal:

```bash
ros2 run demo_nodes_cpp listener
```

You should see ROS nodes communicating.

---

## 📝 Notes:

* Always source your workspace:

  ```bash
  source ~/ros2_ws/install/setup.bash
  ```

* Use `ros2 doctor` to diagnose setup issues.

* Consider using `tmux` or `terminator` for managing multiple ROS nodes.

---

<h1 align="center">🎯 Task 2.1</h1>

### **Problem Statement:**

Create a simple ROS 2 application using Python in which:

1. A **publisher node** continuously publishes the message:

   ```
   "Hi, My Name is <your_name>."
   ```

   to a topic named `/greeting` at a 1 Hz frequency.

2. A **subscriber node** subscribes to the `/greeting` topic and performs the following:

   * Displays the message received.
   * Maintains and displays a running count of how many times the message has been received.

---

#### **Expected Output Example:**

```text
[INFO] [talker]: Publishing: "Hi, My Name is Alice."
[INFO] [listener]: I heard: "Hi, My Name is Alice." | Count: 1
[INFO] [listener]: I heard: "Hi, My Name is Alice." | Count: 2
...
```

---

### ✅ Requirements:

* Use ROS 2 Humble on Ubuntu 22.04
* Use Python (`rclpy`)
* Topic name must be `/greeting`
* Use `std_msgs/msg/String` message type

---

# Task: [Task 2.1](https://github.com/ShaneshrajeK/Aero_Modelling_Club_Summer_Camp_2025/blob/main/Week_2/task1.md)

---

# Next: [Gazebo Simulator Installation](https://github.com/ShaneshrajeK/Aero_Modelling_Club_Summer_Camp_2025/blob/main/Week_2/gazebo.md)

---
