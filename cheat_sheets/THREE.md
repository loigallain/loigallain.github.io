# THREE.js 

## What is it
three.js is an open source initiative to provide the community with javascript library for uisng webgl primitives in javascript
it implements the usual scheme with a scene, a renderer and various view point
scene follows the scenegraph pattern

## where to find it:
[here](https://threejs.org/) 

## some useful links

define the size of the canvas to adjust to one set by css engine
Arguably the best way to resize three.js use to code it so it just accepts whatever size the canvas is as set by CSS. That way, no matter how you use the canvas your code will work, no need to change it for different situations.

First off when setting the initial aspect ratio there's no reason to set it because we're going to set it in response to the size of the canvas being different so it's just a waste of code to set it twice
````javascript
// There's no reason to set the aspect here because we're going
// to set it every frame anyway so we'll set it to 2 since 2
// is the the aspect for the canvas default size (300w/150h = 2)
const camera = new THREE.PerspectiveCamera(70, 2, 1, 1000);
Then we need some code that will resize the canvas to match its display size

function resizeCanvasToDisplaySize() {
  const canvas = renderer.domElement;
  // look up the size the canvas is being displayed
  const width = canvas.clientWidth;
  const height = canvas.clientHeight;

  // adjust displayBuffer size to match
  if (canvas.width !== width || canvas.height !== height) {
    // you must pass false here or three.js sadly fights the browser
    renderer.setSize(width, height, false);
    camera.aspect = width / height;
    camera.updateProjectionMatrix();

    // update any render target sizes here
  }
}
````

Call this in your render loop before rendering
````javascript
function animate(time) {
  time *= 0.001;  // seconds

  resizeCanvasToDisplaySize();

  mesh.rotation.x = time * 0.5;
  mesh.rotation.y = time * 1;

  renderer.render(scene, camera);
  requestAnimationFrame(animate);
}

requestAnimationFrame(animate);
````
Here's 3 examples, the only difference between the 3 examples is the CSS and whether we make the canvas or three.js makes the canvas

Example 1: fullscreen, We make the canvas

Show code snippet

Example 2: fullscreen canvas, three.js makes the canvas

Show code snippet

Example 3: inline canvas

Show code snippet

Example 4: 50% width canvas (like a live editor)

Show code snippet

notice window.innerWidth and window.innerHeight are never referenced in the code above and yet it works for all cases.


## Introduction


## with Angular

1. install the package
   ````ps
   npm install three
   ````
2. create a component where to draw
   this component will refer to a service where the entire engine will be defined

   ````javascript
   export class World3dComponent implements OnInit {

  @ViewChild('rendererCanvas', {static: true})
  public rendererCanvas: ElementRef<HTMLCanvasElement>;

  public constructor(private three: ThreeEngineService ) { }

  public ngOnInit(): void {
    this.three.createScene(this.rendererCanvas);
    this.three.animate();
  }
    }
````
one sees the reference to a viewhild: the ``rendererCanvas``. This one is important, as a canvas is required for the engine to draw the element.
````html
<div class="engine-wrapper">
  <canvas #rendererCanvas id="renderCanvas"></canvas>
</div>
````

Let's not forget to create the required service:
ThreeEngineService will actually contain the code for scene management.
Let's add a simple cube in it.

````javascript
import * as THREE from 'three';
import { Injectable, ElementRef, OnDestroy, NgZone } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class ThreeEngineService implements OnDestroy {
  private canvas: HTMLCanvasElement;
  private renderer: THREE.WebGLRenderer;
  private camera: THREE.PerspectiveCamera;
  private scene: THREE.Scene;
  private light: THREE.AmbientLight;

  private cube: THREE.Mesh;

  private frameId: number = null;

  public constructor(private ngZone: NgZone) {}

  public ngOnDestroy(): void {
    if (this.frameId != null) {
      cancelAnimationFrame(this.frameId);
    }
  }

  public createScene(canvas: ElementRef<HTMLCanvasElement>): void {
    // The first step is to get the reference of the canvas element from our HTML document
    this.canvas = canvas.nativeElement;

    this.renderer = new THREE.WebGLRenderer({
      canvas: this.canvas,
      alpha: true,    // transparent background
      antialias: true // smooth edges
    });
    this.renderer.setSize(window.innerWidth, window.innerHeight);

    // create the scene
    this.scene = new THREE.Scene();

    this.camera = new THREE.PerspectiveCamera(
      75, window.innerWidth / window.innerHeight, 0.1, 1000
    );
    this.camera.position.z = 5;
    this.scene.add(this.camera);

    // soft white light
    this.light = new THREE.AmbientLight( 0x404040 );
    this.light.position.z = 10;
    this.scene.add(this.light);

    const geometry = new THREE.BoxGeometry(1, 1, 1);
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    this.cube = new THREE.Mesh( geometry, material );
    this.scene.add(this.cube);

  }

  public animate(): void {
    // We have to run this outside angular zones,
    // because it could trigger heavy changeDetection cycles.
    this.ngZone.runOutsideAngular(() => {
      if (document.readyState !== 'loading') {
        this.render();
      } else {
        window.addEventListener('DOMContentLoaded', () => {
          this.render();
        });
      }

      window.addEventListener('resize', () => {
        this.resize();
      });
    });
  }

  public render(): void {
    this.frameId = requestAnimationFrame(() => {
      this.render();
    });

    this.cube.rotation.x += 0.01;
    this.cube.rotation.y += 0.01;
    this.renderer.render(this.scene, this.camera);
  }

  public resize(): void {
    const width = window.innerWidth;
    const height = window.innerHeight;

    this.camera.aspect = width / height;
    this.camera.updateProjectionMatrix();

    this.renderer.setSize( width, height );
  }
}

````

Add further extension (or examples in three), use the Three-full package
````ps
npm install --save three-full
````

then modify the config file with 
````json
    "lib": [
      "es2018",
      "dom"
    ],
    "paths": {
      "three-full": ["node_modules/@types/three"]
    }
 ````
