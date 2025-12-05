# GolfRobotSim

This repository contains the foundations for developing and training a reinforcement-learning based model that controls a 2-wheel autonomous robot designed to collect golf balls on a driving range.  
The simulation serves as a testbed for path planning, environment mapping, obstacle avoidance and efficient ball collection.  
Later, the trained model and software architecture will be transferred to a real physical robot.

---

## 1. Hardware Concept (Real Robot)

The final physical robot is planned to use:
1. **Two motorized wheels** on the left and right side.
2. **A third passive wheel/roller**, identical in width to the robot chassis, which also serves as the ball-pickup mechanism.
3. **A camera system** for:
   - semantic segmentation (terrain, fences, obstacles, no-go zones)
   - object detection (golf balls, hazards)
4. **A Raspberry Pi** for sensor processing, mapping (2D/3D), and path planning.
5. **(Optional) AHRS sensor** for orientation.
6. **GPS module** for global positioning.

---

## 2. Important Real-World Considerations

1. **Balance is not required**, as the robot has a third wheel/roller.
2. **Terrain is uneven** in real life.  
   The simulation should include slopes to train the model for uphill/downhill navigation.
3. **Obstacle collisions are possible and dangerous.**  
   The simulation must allow collisions so the model can learn to avoid them.
4. **No-go zones** should be drivable but penalized with negative reward to mimic real conditions.

---

## 3. Standard Workflow / Behavior Logic

1. The robot starts mapping immediately to determine its surroundings and the base position.
2. It begins **inside the base**, exits the base with a backwards 90° maneuver.
3. It drives **around the entire field border** once to create an initial environmental map.
4. After mapping, it begins **lawn-mower-style up-and-down traversal** to collect golf balls.
5. At the end of the sweep, it returns to the base for unloading.

---

## 4. Training Modes

To maximize model performance, several training scenarios are required:

### **1. Path-Planning Training**
- The robot knows all ball positions and world objects.
- The goal is to generate an optimal picking-path.
- A user manually validates paths to improve the model.

### **2. Blind-Start Training**
- The robot starts with **no knowledge** of balls, borders, or obstacles.
- Only when a ball is detected, its position becomes known.
- Picked balls must be flagged so the robot does not revisit them.

### **3. Partial-Knowledge Training**
- Borders, base, and obstacles are known from the start.
- Ball positions are unknown until detected.
- Picked balls must be tracked with a persistent flag.

### **4. User-Guided Training**
- A user draws recommended paths manually.
- The model learns from these positive demonstrations.

---

## 5. Goal of the Repository

The repository is intended to grow through many incremental issues/tickets.  
This README only provides a technical overview — detailed tasks follow in the issue tracker.

