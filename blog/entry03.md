# Entry 3
##### 2/2/26

## Content
So far, I have been reading the Phaser documentation and experimenting with the example code that it has. When I find a new concept in the documentation I copy the sample code into my own files and then change different parts of it to see how it works. For example, when I was learning about cameras I tested different functions like `setBounds`, `startFollow`, and `setDeadzone` to see how they affected the way the camera moves. I also practiced creating animations, adding audio, and using arcade physics by following the structure from the documentation and slowly building on it. Watching YouTube videos has also helped because they show how real game developers use Phaser in making games, which I further used other games codes to learn more about phaser. Most of my learning has been trial and error. If something doesn’t work I debug. This process has helped me become more comfortable with phaser.

Evidence:
Here are some examples of the code I have worked with while learning phaser:

Audio Code
```language
const music = this.sound.add('bgMusic', {
  loop: true,
  volume: 0.5
});
music.play();
```
This taught me how to load and play background music and sound effects.
Arcade Physics Code
```language
this.player = this.physics.add.sprite(400, 300, 'player');
this.player.setCollideWorldBounds(true);
this.physics.add.collider(this.player, this.platform);
```
This code helped me learn how to give sprites physics and make them collide with platforms.



[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
