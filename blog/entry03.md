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

The next thing I plan to learn about Phaser is player inputs. I want to focus on using keyboard input to move the player and adding a simple start screen.

## Sources
* [Phaser Documentation](https://docs.phaser.io/)
* Youtube videos
* Existing phaser games

## EDP
Right now I am in the "Research the problem" stage of the engineering design process. I am still learning how Phaser works and figuring out what tools and features I need for my platformer game.

## Skills
One skill I have improved is problem decomposition. I break big tasks into smaller pieces. Instead of trying to make a whole game I focus on one part at a time like learning cameras then animations then physics. Another skill is debugging. Many times my code doesn’t work at first so I have to debug and tinker with small changes to my code. I have also practiced time management. I try to schedule time to work on my project and focus on building toward an MVP. This helps me make progress instead of waiting until the last minute.

[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)
