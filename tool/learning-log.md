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

### 10/20/25:

# LL2
#### [Source](https://docs.phaser.io/phaser/concepts/animations)

## Animations

### Creating and Playing Animations

* `this.anims.create(config)` – makes a new animation and stores it by a key (name).
* `sprite.play(key)` – plays an animation that you already created.
* `anims.generateFrameNumbers(key, config)` – helps make animations from sprite sheets by picking frames in order.
* `repeat` and `frameRate` – control how many times the animation loops and how fast it plays.

Example:

```language
class MyScene extends Phaser.Scene {
  preload() {
    this.load.spritesheet('player', 'player.png', {
      frameWidth: 32,
      frameHeight: 48
    });
  }

  create() {
    // Create an animation called 'walk'
    this.anims.create({
      key: 'walk',
      frames: this.anims.generateFrameNumbers('player', { start: 0, end: 3 }),
      frameRate: 10,
      repeat: -1 // loops forever
    });

    // Add the sprite and play the animation
    const player = this.add.sprite(100, 100, 'player');
    player.play('walk');
  }
}
```

### 11/16/25:

# LL3

## Audio

### Loading, Creating, and Playing Audio

* `this.sound.add(key, config)` - Creates a new sound instance in the scene. You use the key you loaded in `preload()`.
* `sound.play()` - Plays the sound you added. You can also play audio directly with `this.sound.play(key, config)` without creating a variable.
* `this.load.audio(key, urls)` - Loads audio files into the game. Phaser accepts multiple formats for browser compatibility.
* `loop` and `volume` - Control whether the audio repeats and how loud it is.

Example:

```language
class MyScene extends Phaser.Scene {
  preload() {
    // Load audio (mp3 + ogg for compatibility)
    this.load.audio('bgMusic', ['bgMusic.mp3', 'bgMusic.ogg']);
    this.load.audio('jump', ['jump.mp3', 'jump.ogg']);
  }

  create() {
    // Create background music sound object
    const music = this.sound.add('bgMusic', {
      loop: true,    // play forever
      volume: 0.5    // half volume
    });

    // Play background music
    music.play();

    // Create a sound effect
    const jumpSound = this.sound.add('jump');

    // Example usage: play the jump sound when SPACE is pressed
    this.input.keyboard.on('keydown-SPACE', () => {
      jumpSound.play();
    });
  }
}
```
