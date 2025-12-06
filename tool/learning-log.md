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

### 11/23/25:

# LL4

## Actions

* `Phaser.Actions.RotateLeft(items, value)` – Rotates all objects left by a certain amount.
* `Phaser.Actions.RotateRight(items, value)` – Rotates all objects right.
* `Phaser.Actions.IncXY(items, x, y)` – Changes (adds to) the X and Y positions of all items.
* `Phaser.Actions.SetXY(items, x, y, stepX?, stepY?)` – Positions all objects starting from a point, optionally spacing them out.
* `Phaser.Actions.ScaleXY(items, value)` – Scales all objects.
* `Phaser.Actions.WrapInRectangle(items, rect)` – Keeps objects inside a rectangle by wrapping them.

Example:

```language
class MyScene extends Phaser.Scene {
  create() {
    // Create a group of images
    this.stars = this.add.group();

    for (let i = 0; i < 20; i++) {
      this.stars.add(
        this.add.image(
          Phaser.Math.Between(50, 750),
          Phaser.Math.Between(50, 550),
          'star'
        )
      );
    }

    // Rectangle boundary to keep objects inside
    this.bounds = new Phaser.Geom.Rectangle(0, 0, 800, 600);
  }

  update() {
    // Move all stars diagonally down-right
    Phaser.Actions.IncXY(this.stars.getChildren(), 1, 1);

    // Wrap them back into the screen when off bounds
    Phaser.Actions.WrapInRectangle(this.stars.getChildren(), this.bounds);
  }
}
```

### 12/7/25:

# LL5

## Display

* `alpha` / `setAlpha(value)` - controls transparency (0 = invisible, 1 = fully visible).
* `blendMode / setBlendMode(mode)` - controls how a game object’s colors blend with the background.
* `setScale(x, y)` / `scaleX` / `scaleY` - changes the size of the object on the screen.
* `rotation` / `setRotation(radians)` / `setAngle(degrees)` - rotates the object around its origin.
* `setX(x) / setY(y) / setPosition(x, y)` - set the location of the object on screen.
* `visible` / `setVisible(true/false)` - whether the object is drawn or hidden.
* `displayWidth` and `displayHeight` - the actual displayed size, which depends on the object’s base size and its scale.

Example:

```language
class MyDisplayScene extends Phaser.Scene {
  create() {
    // Add a sprite (or image) to the scene
    const star = this.add.sprite(400, 300, 'star');

    // Set appearance
    star.setAlpha(0.7);                   // make it somewhat transparent
    star.setScale(1.5);                   // scale it 1.5× original size
    star.setBlendMode(Phaser.BlendModes.ADD);  // change how it blends with background
    star.setVisible(true);                // make sure it's visible
  }

  update() {
    // Animate: rotate slowly, maybe pulse scale or fade
    star.rotation += 0.01;               // rotate a little every frame
  }
}
```
