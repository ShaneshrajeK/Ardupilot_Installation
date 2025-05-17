<h1 align="center"><b> Task 2.2: Integrating ArduPilot, Gazebo, and ROS 2 Using Micro XRCE-DDS </b></h1>

#### 🎯 **Objective:**

Set up a simulated drone environment using ArduPilot, Gazebo, and ROS 2 Humble. Use Micro XRCE-DDS to send commands via a Python ROS 2 node to control a drone.

---

### ✅ **Task Breakdown**

1. **Installation and Setup**

   * Install **ROS 2 Humble** on Ubuntu 22.04.
   * Build and install **ArduPilot SITL** from source.
   * Install **Gazebo Harmonic** and ensure it integrates with ArduPilot using the `ardupilot_gazebo` plugin.
   * Install and run **Micro XRCE-DDS Agent**.

2. **Simulation Environment**

   * Launch the **`runway.world`** in Gazebo.
   * Spawn an **Iris drone** using ArduPilot SITL configured for Gazebo (model: `gazebo-iris`).
   * Ensure communication between ArduPilot and ROS 2 is established using **Micro XRCE-DDS**.

3. **Python ROS 2 Node**

   * Write a ROS 2 Python script using `rclpy` that:

     * Sends a **takeoff command** to 10 meters altitude.
     * Sends a **navigation (waypoint) command** to position `(5, 0, 0)`.
     * Sends a **landing command** once the drone reaches the waypoint.
   * Use **Micro XRCE-DDS** (e.g., via `rclc` compatible topics or bridges) to ensure messages are transmitted from ROS 2 to ArduPilot.

4. **Demonstration**

   * Run the simulation.
   * Show the drone taking off, moving to `(5, 0, 0)`, and landing.
   * Validate using ROS 2 topic echo or Gazebo UI that the drone responds to all commands.

---

### 📦 **Deliverables**

* Python script with the full control logic.
* A short video or screen recording of the simulation.
* Screenshots of:

  * ROS 2 topic list.
  * ArduPilot SITL running.
  * Gazebo with Iris in the runway world.

---

### Submission Link: [Submit Here](https://forms.gle/Wj3ZGBvsJzBxJSJq8)
