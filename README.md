# fpsObserver (fps-observer) : JS Framerate monitoring 

This simple **crossbrowser** library helps you to monitor the window global **framerate**, or your individual animation loops framerates. Each instance of the observer returns an object containing some useful methods, and a stabilized (averaged) FPS value obtained by involving multiple samples (configurable ammount), with **accurate values**, based in calculations from timestamps from the accurate `performance.now()`.

See an example  **visual FPS graph** in action [here](http://colxi.info/fps-observer/test/)

> Note: This library does not provide any GUI element for FPS visualization, but an Object instead with all the framerate information.

## Usage examples 
**Automatic mode :** 
```javascript
import {fpsObserver} from './fps-observer.is';

let myAnimationFPS = new fpsObserver();

// create an animation loop 
function myLoop(){
    console.log( 'Framerate :' , myAnimationFPS.value );
    
    /* perform your canvas drawing... */
    
    requestAnimationFrame( myGameLoop );
};
myLoop();
```


**Manual mode :** 
```javascript
import {fpsObserver} from './fps-observer.is';

let myAnimationFPS = new fpsObserver();
myAnimationFPS.auto = false; // disable auto mode

// create an animation loop 
function myLoop(){
    myAnimationFPS.tick(); // trigger a new tick
    console.log( 'Framerate :' , myAnimationFPS.value );

    /* perform your canvas drawing... */

    requestAnimationFrame( myGameLoop );
};
myLoop();
```

## Constructor Syntax :

```javascript
new fpsObserver( autoMode ); 
```
Parameters : 
- **autoMode** : Boolean to set the status of the automatic mode ( default : true )

Returns:
- new fpsObserver instance object 


## Properties and methods : 

The fpsObserver Constructor will create and init a new observer instance  and return an object with the following properties and methods :

- **fpsObserver.prototype.value** : Holds the averaged value of the framerate 
- **fpsObserver.prototype.auto** : Enable/disable the automatic mode (default : true)
- **fpsObserver.prototype.sampleSize** : Integer to define the ammount of samples to collect to average the FPS ( default : 30 )
- **fpsObserver.prototype.reset()** : Reset the samples collection. Useful after resuming a paused loop
- **fpsObserver.prototype.disconnect()** : Disables the Observer
- **fpsObserver.prototype.tick()** : Method to call manually in each Animation loop cycle, when automatic mode is disabled. It keeps track of each cycle times. 


# Package distribution 

This library can be obtained using any of the following methods : 

**Npm** : Install using the package manager 
```bash
$ npm install fps-observer -s
```

**Git** : Clone from Github... (Or download the latest release [here](https://github.com/colxi/fps-observer/releases/latest))
```bash
$ git clone https://github.com/colxi/fps-observer
```

**CDN** : Inlcude the latest release of the library in your HTML head
> Warning : Not recomended for production enviroments!
```html
<script src="https://colxi.info/fps-observer/src/main.js"></script>
```

> Note : When included in the HTML `head`, the fpsObserver constructor becomes available as `window.fpsObserver`
