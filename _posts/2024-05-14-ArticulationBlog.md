---
toc: false
comments: false
layout: post
title: Articulation Blog
description: Articulation Blog
type: ccc
courses: { csse: {week: 7} }
---

> # JavaScript GameObjects to GameLevel
- For our objects, we have made many new sprites and added several new pieces of code. Our player is called "Escaper" and our enemies are called "SkibidiToilet". Our main feature of our level is the Skibidi titan. 
    - Skibidi Titan has its own sprite, sound, and code(SkibidiTitan.js).
- We also added our own collisions using the code from PlayerHills.js and named it PlayerSkibidi.js to detect the collisions from the laser from the skibidi titan, skibidi toilets, and the ending screen. We had called these in the GameSetup.js.
    - GameSetup.js makes the maps using the GameLevel.js which gathers all of the objects in a given array and will make the objects accordingly.

```js
// GameSehup.js Key objective is to define GameLevel objects and their assets.
import GameEnv from './GameEnv.js';
import GameLevel from './GameLevel.js';
// To build GameLevels, each contains GameObjects from below imports
import Background from './Background.js'
import BackgroundHills from './BackgroundHills.js';
import BackgroundMountains from './BackgroundMountains.js';
import BackgroundTransitions from './BackgroundTransitions.js';
import BackgroundClouds from './BackgroundClouds.js';
import Platform from './Platform.js';
import JumpPlatform from './JumpPlatform.js';
import Player from './PlayerBase.js';
import PlayerHills from './PlayerHills.js';
import PlayerSkibidi from './PlayerSkibidi.js'; //PlayerSkibidi is for the collisions in the skibidi level.
import Tube from './Tube.js';
import Tree from './Tree.js';
import Goomba from './Goomba.js';
import FlyingGoomba from './FlyingGoomba.js';
import BlockPlatform from './BlockPlatform.js';
import Mushroom from './Mushroom.js';
import Coin from './Coin.js';
import FlyingUFO from './FlyingUFO.js';
import Alien from './Alien.js';
import GameControl from './GameControl.js';
import skibidiTitan from './SkibidiTitan.js'; //SkibidiTitan is for the skibidi titan in the skibidi level.
import Laser from './Laser.js'; //Laser is for the laser that the skibidi titan shoots which is meant to kill the player/
import SkibidiToilet from './SkibidiToilet.js'; //SkibidiToilet is for the skibiditoilet enemy which is used in skibidi level.

```

># Game Level Creation
- To make a new level, we made an array filled with objects that has their own variables like their position, name, id, and data.
- To actually make the level into the game, we used the GameLevel.js and fed our array into GameLevel.js.

<br>

## DrawIO Diagram of how it works:
![DrawIO Diagram of GameObject stuff.]({{site.baseurl}}/images/diagramforcsse2final.drawio.png)


<br>
<hr>
<br>
<br>

# Finite State Machines

<br>

```js
//Skibidi Toilet Level
    const skibidiGameObjects = [
      // GameObject(s), the order is important to z-index...
      { name: 'desert', id: 'background', class: Background, data: this.assets.backgrounds.desert },
      //{ name: 'clouds', id: 'background', class: BackgroundClouds, data: this.assets.backgrounds.clouds },
      { name: 'skibidiTitan', id: 'skibidiTitan', class: skibidiTitan, data: this.assets.enemies.skibidiTitan, xPercentage:  0.35, yPercentage: 0.5, minPosition: 0.5 }, 
      { name: 'sand', id: 'platform', class: Platform, data: this.assets.platforms.sand },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.2, yPercentage: 1 },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.4, yPercentage: 0.6 },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.325, yPercentage: 0.8 },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.2, yPercentage: 0.5 },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.225, yPercentage: 0.5 },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.0, yPercentage: 0.5 } ,
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.025, yPercentage: 0.5 },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.025, yPercentage: 0.5 },
      { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.sand, xPercentage: 0.5, yPercentage: 0.5 },
      ///{ name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.475, yPercentage: 0.5 },
      { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.325, yPercentage: 0.7 },
      { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: -0.0125, yPercentage: 0.4 },
      { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.0125, yPercentage: 0.4 },
      { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.0325, yPercentage: 0.4 },
      { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.3, minPosition: 0.07 },
      { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.5, minPosition: 0.3 },
      { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.75, minPosition: 0.5 }, //this special name is used for random event 2 to make sure that only one of the Goombas ends the random event
      { name: 'escaper', id: 'player', class: PlayerSkibidi, data: this.assets.players.escaper  },
      { name: 'laser', id: 'Laser', class: Laser, data: this.assets.obstacles.laser, xPercentage:  0.75, yPercentage: 0.5 },
      { name: 'toiletTube', id: 'toiletEnd', class: Tree, data: this.assets.obstacles.toilet },
      { name: 'complete3', id: 'background', class: BackgroundTransitions,  data: this.assets.backgrounds.complete3 },
    ];

    new GameLevel( {tag: "skibidi", callback: this.playerOffScreenCallBack, objects: skibidiGameObjects} );

```

<br>
<br>

# Objects in JS

<br>

- A brief explanation: An object is like a table. Just as a table holds values, an object holds tables and can also be changed. An example of this would be the following code:
```js
 const carTable = ["Honda", "Civic", 2000]; // Table
 const carObject = {Company:"Honda", Model:"Civic", Year:2000} //Object
 console.log(carTable); //Output: (3) ["Honda", "Civic", 2000]
 console.log(carObject); //Output: (3) {Company: "Honda", Model: "Civic", Year: 2000}
 console.log(carTable[0]); //Output: "Honda"
 console.log(carObject.Company); //Output: "Honda"
 //To change the year:
 console.log("Current Year: Table:"+carTable[2]+" Object:"+carObject.Year); //Output: Current Year: Table:2000 Object:2000
 carTable[2] = 2024 //Table
 carObject.Year = 2024 //Object
 console.log("Updated Year: Table:"+carTable[2]+" Object:"+carObject.Year); //Output: Updated Year: Table:2024 Object:2024
 ```
 ## Object are also able to hold functions!
 ```js
 const mathObject = {
                        add:function(num1, num2){
                            return num1 + num2;
                        },
                        square:function(num){
                            return num * num;
                        }
                    }
 console.log(mathObject.add(5,10)); //Output: 15
 console.log(mathObject.square(5)); //Output: 25
 console.log(mathObject.add(29,mathObject.square(32))) //Output: 1053
 ```
 - Object in our game: (`GameSetterSkibidi.js`)
    - This object creates the skibidi titan boss that is in our level. The name gives the name, id is the id, class is the class for the code to get, data is the sprite animation, xPercentage is the x position ratio on the canvas, and yPercentage is the y position ratio on the canvas.
 ```js
 {name: 'skibidiTitan', id: 'skibidiTitan', class: skibidiTitan, data: this.assets.enemies.skibidiTitan, xPercentage:  0.35, yPercentage: 0.5, minPosition: 0.5 }
 ```

 <br>
 <br>

 # Single Responsibility Principal

 <br>
 
 - Here is an example of the Single Responsibility Principal inside of our level in the game (`PlayerSkibidi.js`):
    - Every `this.handleCollisionEvent("");` has their own responsibility in the game. This is what makes the collision work in our game.
 ```js
    handleCollisionStart() {
        super.handleCollisionStart(); // calls the super class method
        // adds additional collision events
        this.handleCollisionEvent("finishline");
        this.handleCollisionEvent("SkibidiToilet");
        this.handleCollisionEvent("laser");
    }
 ```


<br>
<hr>
<br>
<br>

> # Things I have learned throughout Trimester 3 CSSE2 class
- ## I have learned several different things about coding and the fundamentals.
    - One of the major things I have learned about this year is Object Oriented Programming. Previously, I always had dodged OOP because I had always thought it was too complicated to learn and I was very lazy. Fortunately, this class had given me the right materials and knowledge to learn OOP.
    - 
    - Another thing I had learned about is the difference between variables local to the script, and throughout the machine. Previously on my skibidi titan, I had used variables by typing "var 'variablename' = ;" and Mr. Mortensen had told me that it is not good to program like this given our circumstances. Therefore he taught me how to make variables inside of the objects. So instead of making a variable for the laser like, "var Laser = document.getElementById("Laser");", instead he had told me to write it like this, "this.Laser = document.getElementById("Laser");" inside of the constructor.
    - 
    - I had also learned about making positions based on ratios rather than a fixed number. This is because my skibidi titan was having trouble scaling to the screen because I had it on a fixed number that only looked good on my screen, but on other screens it was way off. To combat this issue, I had discovered ratios with the help of Mr. Mortensen to make the skibidi titan fit on everyone's screen.
    - 
    - Finally, one of the most important things I had learned is using GitHub. I had never realized that you can make your own websites/games on Github because I always thought it was just for sharing code with others. I had never known how to use git or any of those features until I had reached this class. This class has taught me a lot about the tools computer engineers use.

> # My favorite addition tot he game
- ## My skibidi titan I had made is what I am most proud of making in this class
    - This skibidi titan is complex due to it running off of several different files for player position along with the addition of another sprite which is the laser.
    - One of the biggest struggles I had faced with the titan was the ratios because I had never known how to do the ratios until just recently.
    - A big thing that was my biggest accomplishment with the titan would be the charging up effects along with the shooting of the laser. The charging up effects include the inverting of the sprite and 2 audio cues, the charge and the fire sounds.
    - Here is the entire piece of code for the skibidi titan in `SkibidiTitan.js`:

```js
import Character from './Character.js';
import GameEnv from './GameEnv.js';
import GameControl from './GameControl.js';
import Laser from './Laser.js';


export class skibidiTitan extends Character {
    // constructors sets up Character object 
    constructor(canvas, image, data, xPercentage, yPercentage, name, minPosition){
        super(canvas, image, data);

        //Unused but must be Defined
        this.name = name;
        this.y = yPercentage;

        //Initial Position of Goomba
        this.x = xPercentage * GameEnv.innerWidth;

        //Access in which a Goomba can travel    
        this.minPosition = minPosition * GameEnv.innerWidth;
        this.maxPosition = this.x + xPercentage * GameEnv.innerWidth;

        this.immune = 0;
        this.debounce = 0;
        this.laser = document.getElementById("Laser");
        this.laserHeight = this.laser.innerHeight

    }
    
    killBeam(target) {
        if (target.timer === false) {
            target.timer = true;
            if (GameEnv.difficulty === "normal" || GameEnv.difficulty === "hard") {
                target.canvas.style.transition = "transform 0.5s";
                target.canvas.style.transform = "rotate(-90deg) translate(-26px, 0%)";
                GameEnv.playSound("PlayerDeath");

                if (target.state.isDying == false) {
                    target.state.isDying = true;
                    setTimeout(async() => {
                        await GameControl.transitionToLevel(GameEnv.levels[GameEnv.levels.indexOf(GameEnv.currentLevel)]);
                        console.log("level restart")
                        target.state.isDying = false;
                    }, 900); 
                }
            } else if (GameEnv.difficulty === "easy") {
                this.x += 10;
            }
        }
    }

    update() {
        super.update();
        this.immune = 1;
        if(this.debounce < 240 && this.debounce > -1){
            this.laser.style.left = `-2000px`;
            this.x = GameEnv.PlayerPosition.playerX - 0.14*GameEnv.innerWidth;
            this.debounce += 1;
        }
        if(this.debounce < -120){
            this.debounce += 1;
            if(this.debounce == -235){GameEnv.playSound("laserCharge");this.laser.style.transform = `scaleY(${0})`;}
            this.canvas.style.filter = `invert(${this.debounce+240}%)`
        }else if(this.debounce < 0 && this.debounce >= -120){
            this.debounce += 1;
            this.canvas.style.filter = `invert(0%)`;
            this.laser.style.left = `${this.x + 0.14*GameEnv.innerWidth}px`;
            
            
            this.laser.style.transform = `scaleY(${(this.debounce+120)/40})`;
            this.laser.style.top = `${(this.debounce+120)*6}px`;
            if(this.debounce == -115){GameEnv.playSound("laserSound");}

            var plrPos = GameEnv.PlayerPosition.playerX;
           
            if (this.x >= plrPos - 250 && this.x <= plrPos - 150) {
                //setTimeout(Plr.goombaCollision.bind(this), 50);
                this.killBeam(GameEnv.player);
                this.debounce = 0;
                this.laser.style.left = `${this.x + 0.14*GameEnv.innerWidth}px`;
            }
        }

        if(this.debounce == 240){
            this.debounce = -240;
        }
        //console.log((GameEnv.PlayerPosition.playerX - 200) + " " + this.x);
        
        
        
        //Immunize Goomba & Texture It
        if (GameEnv.difficulty === "hard") {
                this.canvas.style.filter = "invert(100%)";
                this.canvas.style.scale = 1.25;
                this.immune = 1;
        } else if (GameEnv.difficulty === "impossible") {
            this.canvas.style.filter = 'brightness(1000%)';
            this.immune = 1;
        }

        // Move the enemy
        //this.x -= this.speed;
        this.y = 0.25*GameEnv.innerHeight;
        this.playerBottomCollision = false;


        
    }
}

export default skibidiTitan;
```
