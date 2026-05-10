# Glacier Run

Glacier Run is a 3D platforming game developed for the Proteus controller (using the FEH libraries). Players navigate a polar bear across melting ice floes, avoiding freezing water to reach the safety of the goal flag. Rather than using existing game engines or graphics APIs, this project features a custom-built **3D Software Renderer**, a **Polygon-Level Physics Engine**, and a **Multi-threaded Pipeline** designed to maximize performance on resource-constrained hardware.

## 🎮 Game Features
- **Custom 3D Engine:** A software-based renderer featuring lighting, refraction, and parallelized projection using multi-threading.
- **Physics System:** Realistic gravity, drag, and collision detection against 3D polygons.
- **Dynamic Environment:** Animated water waves and falling snow particles.
- **Multiple Stages:** Three distinct levels of increasing difficulty.
- **Multimedia Experience:** Includes custom menu art, cutscenes, and a full soundtrack with sound effects.

## 🚀 Engineering Highlights

### 1. Custom 3D Software Rasterizer
The core of this project is a software-based graphics pipeline that transforms raw 3D geometry into screen-space pixels without the aid of a GPU (OpenGL/DirectX).
- **Parallelized Pipeline:** Leverages Windows threading to distribute vertex projection and lighting calculations across multiple CPU cores, mitigating the performance bottlenecks inherent in software rendering.
- **Advanced Optical Simulation:** Implements custom lighting models including specular highlights (`reflectionValue`) and light scattering/refraction to simulate the material properties of ice and water.
- **Scanline Optimization:** Uses a line-based drawing approach to minimize expensive LCD draw calls, ensuring a stable frame rate on limited hardware.

### 2. High-Fidelity Physics & Collision
Developed a custom physics system to handle complex 3D interactions and rigid-body dynamics.
- **Triangle-Mesh Collision:** Collision detection is performed at the polygon level using vector projection and "same-side" testing, allowing the player to navigate complex, non-primitive geometry.
- **Sub-Frame Interpolation:** Implements a movement-stepping algorithm to prevent "tunneling" (objects passing through geometry at high velocities), a common challenge in physics simulation.
- **9-Point Hitbox Dynamics:** Uses a multi-point sampling system for the player character to ensure stable footing and realistic interaction with uneven or slanted terrain.

### 3. Procedural Environmental Systems
- **Vertex Animation:** Real-time water displacement using sine-wave math to simulate fluid movement dynamically within the vertex buffer.
- **Atmospheric Particle Systems:** A snow particle system that manages hundreds of individual points with efficient recycling logic to maintain immersion without exhausting system memory.

## 🛠️ Technical Stack & Architecture
- **Language:** C++
- **Architecture:** Implements a central **Container Pattern** to maintain global state and facilitate communication between decoupled systems (Physics, Renderer, Input).
- **Math Foundation:** Built a custom linear algebra suite for dot products, cross products, and spherical-to-cartesian coordinate transformations.

## 🕹️ Controls
- **WASD:** Move the player.
- **Spacebar:** Jump.
- **Mouse/Touch:** Rotate the camera.
- **ESC:** Pause the game.

## 📁 System Overview
- `renderer.cpp`: Core rasterization logic, scanline drawing, and multi-threaded rendering pipeline.
- `physics.cpp`: Rigid body dynamics, gravity simulation, and polygon collision resolution.
- `data.cpp`: Metadata-driven level loading and dynamic object scaling.
- `environment_effects.cpp`: Procedural wave math and particle physics.
- `utils.cpp`: High-performance math utilities for 3D space transformations.

---
*Developed as part of the FEH Software Development Project.*
