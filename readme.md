# Coincidence
Node.js library for the interupts that count the coincidence and single channel readout.

### Use
For example to use it on your project instatiate the libray, and call the data function. As it acsesses hardware features, you need sudo in order to run it.

The library requires a array of pins with names, there are the pins that interupts are attached to. The pins are the hardware GPIO pins.
```json
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
This array is sent to the constuctor, after importing the library. This pinsts out the coincidence values every minuite.
```js
var Coincidence = require("./coincidence.js");
var coincidence = new Coincidence(pins);
setInterval(function(){
 console.log(coincidence.log()); 
},60000);
```
You can can also call it directly from the command line 

```bash
sudo node -e 'setInterval(function(){console.log(new (require("./coincidence.js"))([["Zero and One", 17], ["Zero and Two", 18],["Zero and Three", 27]]).log())},60000);'
```

### Response
The expected response is a JSON object with the counts every minuite.
```json
{ Zero and One: 560,
  Zero and Two: 455}
```