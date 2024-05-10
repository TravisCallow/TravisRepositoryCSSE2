---
toc: false
comments: false
layout: post
title: Finite State Machine
description: Finite State Machine
type: ccc
courses: { csse: {week: 7} }
---


```js
class water{
    PhasesOfMatter(){
        constructor(){
            this.state = "liquid";
        }
        switch(this.state){
            case "solid":
                console.log("Temperature is dropping to 32 F");
                this.state = "Frozen";
                break;
            case "liquid":
                console.log("Temperature is at 80 F");
                this.state = "Liquid";
                break;
            case "gas":
                console.log("Temperature is rising to 212 F");
                this.state = "Gas";
                break;
        }
    }
}
```

## Objects in JS
- A brief explanation: An object is like a table. Just as a table holds values, an object holds tables. An example of this would be 
```js
 const car = ["Honda", "Civic", "2000"]; // Table

 const car = {brand:"Honda",
             model:"Civic", 
             year:"2000"} //Object
 ```