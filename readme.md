# Coincidence
Node.js library for the interrupts that count the coincidence and single channel readout.

### Use
For example, to use it on your project instantiate the library, and call the data function. As it accesses hardware features, you need sudo to run it. Include it in your `package.json` dependency tree with
```javascript
"dependencies": {
  "coincidence": "muonTelescope/coincidence"
}
```
The library requires an array of pins with names, there are the pins that interrupts are attached to. The pins are the hardware GPIO pins.
```javascript
pins = [
    ['Zero and One'  , 17],
    ['Zero and Two'  , 18],
    ['Zero and Three', 27],
    ['One and Two'   , 11],
    ['One and Three' , 25],
    ['Two and Three' , 09],
    ['Zero'          , 24],
    ['One'           , 23],
    ['Two'           , 22],
    ['Three'         , 10],
];
```
This array is sent to the constructor, after importing the library. This prints out the coincidence values every minute.
```js
var Coincidence = require("coincidence");
var coincidence = new Coincidence(pins);
setInterval(function(){
 console.log(coincidence.log()); 
},60000);
```
You can also call it directly from the command line 

```bash
sudo node -e 'setInterval(function(){console.log(new (require("./coincidence.js"))([["Zero and One", 17], ["Zero and Two", 18],["Zero and Three", 27]]).log())},60000);'
```

### Response
The expected response is a JSON object with the counts every minute.
```javascript
{ Zero and One: 560,
  Zero and Two: 455}
```
