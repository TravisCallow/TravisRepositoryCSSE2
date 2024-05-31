---
toc: false
comments: false
layout: post
title: Articulation Blog
description: Articulation Blog
type: ccc
courses: { csse: {week: 7} }
---

> JavaScript GameObjects to GameLevel
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

>Game Level Creation
- To make a new level, we made an array filled with objects that has their own variables like their position, name, id, and data.
- To actually make the level into the game, we used the GameLevel.js and fed our array into GameLevel.js.

<br>
<hr>
<br>
<br>

- Finite State Machines

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

- Objects in JS

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
 - Object are also able to hold functions!
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

 <br>
 <br>

 - Single Responsibility Principal

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

![DrawIO Diagram of GameObject stuff.]({{site.baseurl}}/images/diagramforcsse2final.drawio.png)

