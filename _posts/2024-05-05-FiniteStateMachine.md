---
toc: false
comments: false
layout: post
title: Finite State Machine
description: Finite State Machine
type: ccc
courses: { csse: {week: 7} }
---

- This finite state machine is an example of the states of water and how water can be either a solid, liquid, or gas depending on it's temperature.

```js
class Water {
    constructor() {
        this.state = "liquid"; //Sets the state
    }
    changeState(temperature) { //Function to set a temperature and it will use if statements to determine if the water will be a liquid, gas, or solid.
        switch (this.state) {
            case "liquid":
                if (temperature > 32 && temperature <212) { //Liquid
                    console.log("Temperature is rising above 32°F");
                    this.state = "liquid";
                }
                break;
            case "solid":
                if (temperature <= 32) { //Solid
                    console.log("Temperature is dropping below 33°F");
                    this.state = "solid";
                } 
                break;
            case "gas":
                if (temperature >= 212) { //Gas
                    console.log("Temperature is rising to 212°F");
                    this.state = "gas";
                }
                break;
        }
    }
}

const water = new Water(); 

console.log("Previous state:", water.state);  //Output: Previous state: liquid
water.changeState(80); //Output: Previous state: Temperature is rising above 32°F
console.log("Current state:", water.state); //Output: Current state: liquid
water.changeState(212); //Output: Previous state: Temperature is dropping below 33°F
console.log("Current state:", water.state); //Output: Current state: gas
water.changeState(10); //Output: Previous state: Temperature is rising to 212°F
console.log("Current state:", water.state); //Output: Current state: solid
```

## Objects in JS
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
 - How we used objects in the level design:
 ```js
//Skibidi Toilet Level
        const skibidiGameObjects = [
          // GameObject(s), the order is important to z-index...
          { name: 'desert', id: 'background', class: Background, data: this.assets.backgrounds.desert },
          //{ name: 'clouds', id: 'background', class: BackgroundClouds, data: this.assets.backgrounds.clouds },
          { name: 'skibidiTitan', id: 'skibidiTitan', class: skibidiTitan, data: this.assets.enemies.skibidiTitan, xPercentage:  0.35, minPosition: 0.5 }, 
          { name: 'sand', id: 'platform', class: Platform, data: this.assets.platforms.sand },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.2, yPercentage: 1 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.4, yPercentage: 0.6 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.325, yPercentage: 0.8 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.2, yPercentage: 0.5 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.225, yPercentage: 0.5 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.0, yPercentage: 0.5 } ,
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.025, yPercentage: 0.5 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.025, yPercentage: 0.5 },
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
- This is what makes the elements in the level. Each element is an object with different values like their position, class, and name.

- Here is an example of a single responsibility principal in our game.
```js
handleCollisionStart() {
        super.handleCollisionStart(); // calls the super class method
        // adds additional collision events
        this.handleCollisionEvent("toiletEnd");
        this.handleCollisionEvent("SkibidiToilet");
        this.handleCollisionEvent("laser");
    }
```