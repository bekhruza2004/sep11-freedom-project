# Tool Learning Log

## Tool: **Phaser**

## Project: **Platformer**

### 10/5/25:

# LL1
#### [Source](https://docs.phaser.io/phaser/concepts/cameras)

## Cameras

### Moving and Positioning the Camera
* `this.camera.main` - gets the main camera
* `camera.setScroll(x, y)` - moves where the camera is looking
* `camera.centerOn(x, y)` - centers the camera on a point
* `camera.setBounds(x, y, width, height)` - keeps the camera inside the game world

```language
class MyScene extends Phaser.Scene {
  create() {
    const cam = this.cameras.main;
    cam.setBounds(0, 0, 2000, 2000); // world size
    cam.setScroll(100, 200);         // move the camera
    cam.centerOn(400, 300);          // center it on a point
  }
}
```
This lets you control exactly what part of your game world is visible. The bounds keep the camera from going off-screen and `centerOn` is good for focusing on a specific area.

### Making the Camera Follow a Player
* `camera.startFollow(target, ..., lerpX, lerpY)` - makes the camera follow something
* `camera.setLerp(x, y)` - controls how smooth the following is
* `camera.setDeadzone(width, height)` - creates a box where small movements don’t shift the camera

```language
class MyScene extends Phaser.Scene {
  create() {
    const cam = this.cameras.main;
    this.player = this.add.sprite(400, 300, 'player');
    cam.setBounds(0, 0, 2000, 2000);
    cam.startFollow(this.player, false, 0.1, 0.1);
    cam.setDeadzone(100, 50);
  }
}
```
Here, the camera smoothly follows the player, but it won’t move unless the player goes outside the 100×50 zone. This helps the camera feel more natural instead of shaky or too fast.





<!-- 
* Links you used today (websites, videos, etc)
* Things you tried, progress you made, etc
* Challenges, a-ha moments, etc
* Questions you still have
* What you're going to try next
-->
