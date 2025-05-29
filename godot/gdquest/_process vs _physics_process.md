

## `_process(delta)`

This function is called **every single frame** your game renders. How often it's called depends on how fast your game is running (your Frames Per Second or FPS).

- **`delta`**: This is a small number representing the time (in seconds) that has passed since the last frame. It's useful for making movement and other actions smooth and independent of the frame rate. For example, instead of moving an object `5 pixels`, you'd move it `speed * delta` pixels.

**Use `_process` for things like:**

- **Input handling**: Checking if a button is pressed.
- **Visual updates**: Changing an animation, updating a score display, moving non-physics-based UI elements.
- **Game logic that doesn't directly involve physics**: Timers, managing game state, AI decision-making (that isn't physics-dependent).
- **Anything that needs to happen as often as possible to look smooth.**

## `_physics_process(delta)`

This function is called at a **fixed interval**, regardless of your game's visual frame rate. By default, it runs 60 times per second, but you can change this in the project settings (Physics -> Common -> Physics Ticks Per Second).

- **`delta`**: This is also the time passed since the last physics update. Because `_physics_process` runs at a fixed rate, this `delta` will (usually) be a consistent value (e.g., 1/60th of a second).

**Use `_physics_process` for things like:**

- **Moving physics bodies**: Anything that uses Godot's physics engine (RigidBody2D/3D, CharacterBody2D/3D, StaticBody2D/3D). This includes applying forces, setting velocities, and collision detection/response.
- **Anything that needs to be synchronized with the physics engine to ensure stable and predictable behavior.**

## For easy to understand

- If it involves moving something that can bump into other things (like a player character that collides with walls, or a ball that bounces), use _physics_process.
- For almost everything else (checking button presses, changing colors, updating text, animations that don't affect collisions), try _process first.
