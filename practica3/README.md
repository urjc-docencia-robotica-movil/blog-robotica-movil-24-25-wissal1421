# Obstacle Avoidance

In this project, I worked with an autonomous car equipped with a laser sensor to navigate an obstacle-filled environment. The goal was for the car to reach specific **waypoints** without colliding with any obstacles. To achieve this, the car combines two forces: an **attractive force** that guides it toward the target and a **repulsive force** that pushes it away from nearby obstacles.

As with any programming project, there were challenges along the way. But these challenges allowed me to learn a lot, especially about how each force is calculated and combined to give direction to the car. Here’s a summary of the problems I encountered and how I solved them.

---

## Problem 1: How to Make the Car "See" Its Target and Obstacles?

The first step was to convert the car's and target’s coordinates into **relative terms**. This was necessary because the target’s information comes in “absolute” coordinates, i.e., fixed positions in the environment, while the car can only "see" in relation to its own position and orientation. Understanding how to transform these coordinates was challenging, as it required accounting for the car’s **orientation angle** (or "yaw") to ensure the car actually “sees” the target as if it were straight ahead. After some trial and error with mathematical functions, I managed to make the target’s position relative to the car.

---

## Problem 2: Processing Laser Sensor Data and Force Calculation

The next step was to **process the data** from the car's laser sensor. The sensor measures the distance to any obstacle at various angles around the car. Initially, I thought of doing the calculations in a single coordinate system, but I quickly discovered this made force calculation difficult. I ended up creating two coordinate systems for the laser data: one polar (distance and angle) and one Cartesian (X and Y positions), which greatly simplified calculating the **repulsive force**.

I encountered an interesting issue here. Since the repulsive force depends on the distance to the obstacle, when obstacles were very close, the repulsive force value shot up, causing the car to make sharp turns. To fix this, I implemented a small **mathematical adjustment** (a kind of damping) that reduced the impact of very close obstacles, improving navigation.

---

## Problem 3: Balancing Attractive and Repulsive Forces

When combining the attractive force that pulls the car toward its target and the repulsive force that pushes it away from obstacles, I found it was easy to end up in a “push-pull” situation where the car barely advanced. If the attractive force was too strong, the car moved forward but ignored obstacles. If the repulsive force was too strong, the car avoided obstacles but didn’t move toward its goal.

The solution I found was to **tweak two "gains"**, essentially multipliers for each type of force. By adjusting these values up and down, I achieved a balance. This allowed the car to move toward its destination and avoid obstacles without veering off course. This helped me better understand the importance of balance in autonomous navigation systems.

---

## Problem 4: Speed Control

One last detail was controlling the car’s **speed**. The linear speed (moving forward) was calculated based on the total force, but capped at a maximum so the car didn’t go too fast when approaching the target. The **angular speed** (turning) was also adjusted based on the angle the car needed to take. Initially, this was tricky because, without well-tuned speed control, the car tended to “oscillate” – moving in circles or zigzagging near obstacles.

After several attempts, I managed to reduce this oscillation by capping the maximum speed and adjusting the angular force calculations a bit. This helped the car make smooth turns and accelerate in a controlled manner.

---

## 📺 Watch the Project in Action

Check out the **video demonstration** of the car navigating its environment with attractive and repulsive forces in real-time! [Click here to watch!](https://drive.google.com/file/d/1tV-_FLCDW3SKL8Z6T9HBhU_FGKyM7qzK/view?usp=sharing)

---
