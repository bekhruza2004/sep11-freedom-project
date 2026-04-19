# Entry 5
##### 4/19/26

## Content

Since last time, I have continued learning Phaser in the same way by using the [documentation](https://docs.phaser.io/phaser/concepts/gameobjects), testing example code, and modifying it to my own game. But now I feel more comfortable experimenting without needing to follow tutorials. I also kept watching YouTube videos to see how developers structure their games especially for adding more advanced features like interactions between objects. While finishing my MVP I learned a lot of new things by actually making my game. One of the things I learned was how to use overlap and collision detection to create interactions like passing the bomb between players. Another important thing I learned was using timers and game state. I created a countdown system for the bomb. This helped me understand how to update things over time. I also learned how to use tweens which I did not know before and it was something I needed for my MVP so I learned it through a few tutorials. I used tweens to create an explosion effect for the bomb. My game now has two players, platforms, a bomb mechanic, a win condition, and a scoreboard. I still need to fix many things in my game before I submit it for my final Freedom Project and if I have time I'm going to add some beyond MVP features to my game that I had planned. Overall, making my game helped me understand Phaser much better.

## Evidence

This is my countdown timer for the bomb for it to explode:

```language
this.lastTimerUpdate += delta;
                if (this.lastTimerUpdate >= 1000) {
                    this.lastTimerUpdate = 0;
                    this.bombTimer--;

                    let color = '#fff';
                    if (this.bombTimer <= 5) {
                        color = '#ff0000';
                    } else if (this.bombTimer <= 10) {
                        color = '#ff9900';
                    }

                    this.timerText.setText('BOMB: ' + this.bombTimer + 's');
                    this.timerText.setColor(color);

                    if (this.bombTimer <= 0) {
                        this.explodeBomb();
                    }
                }
            }
```

This is the tween animation I was talking about where I made an explosion effect for the bomb:

```language
explodeBomb() {
                this.gameStarted = false;

                const explosion = this.add.circle(this.bomb.x, this.bomb.y, 10, 0xff6600, 1);
                this.tweens.add({
                    targets: explosion,
                    radius: 100,
                    alpha: 0,
                    duration: 500,
                    onComplete: () => explosion.destroy()
                });
```

## Sources

I continued using the [Phaser Documentation](https://docs.phaser.io/phaser/concepts/gameobjects) and [YouTube tutorials](https://www.youtube.com/results?search_query=phaser+3+tutorials). However, I learned more from making my own game and solving problems as they came up.

## EDP

I am at the create a prototype and test and evaluate the prototype step of the Engineering Design Process.

## Skills

One skill I improved is problem decomposition because I had to figure out how to connect everything while making my MVP like input and physics so I broke down everything. I also improved my debugging especially when I was working on the interactions like bomb passing and collisions. Another skill I improved is growth mindset because finishing the MVP required me to test and fix many issues until the game worked correctly and I got some help from friends.

[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
