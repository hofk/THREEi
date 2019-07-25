# THREEi
three.js addon for triangulation of implicit surfaces. The addon generates indexed BufferGeometries.

### Publication in progress

#### Algorithmus nach / Algorithm based on E. Hartmann.

The algorithm was originally implemented in Pascal and visualized with POV-Ray.

The implementation of the algorithm with three.js/JavaScript deviates from the template in some places.

de: https://www2.mathematik.tu-darmstadt.de/~ehartmann/cdg0/cdg0n.pdf

en: https://www2.mathematik.tu-darmstadt.de/~ehartmann/cdgen0104.pdf

siehe / see

de: https://de.wikipedia.org/wiki/Implizite_Fl%C3%A4che

en: https://en.wikipedia.org/wiki/Implicit_surface

.................................................................... Sphere with Holes (Triangulation)  ..............................................................................

Sphere with arbitrarily arranged openings, circular or defined by points on the sphere.
The geometry is realized as indexed BufferGeometry.

Algorithm simplified and modified for sphere. 

```javascript

const g = new THREE.BufferGeometry( );
g.createSphereWithHoles = THREEg.createSphereWithHoles;
//g.createSphereWithHoles( detail );
g.createSphereWithHoles( detail, holes );

 ``` 

parameters: 

detail:  Math.PI / detail  is rough side length of the triangles

holes (optional): array of arrays of holes

####  EXAMPLE:

```javascript

const g = new THREE.BufferGeometry( );
const detail = 50;
const holes = [
	// circular hole, 3 elements: [ theta, phi, count ]
	[ 2.44,  0.41, 12 ],
	[ 0.72,  2.55, 19 ],
	[ 1.32, -2.15, 62 ],
	[ 1.82,  0.11, 16 ],
	[ 1.21,  1.23, 13 ],
	[ 2.44,  1.84, 25 ],
	[ 3.05,  3.22, 21 ],
	[ 2.42, -2.61, 14 ],
	// points hole,: array of points theta, phi, ...  (last point is connected to first)
	[ 0,0,  0.5,-0.8,  0.25,-0.27,  0.4,0.3,  0.3,0.72 ]
];

g.createSphereWithHoles = THREEg.createSphereWithHoles;
//g.createSphereWithHoles( detail );
g.createSphereWithHoles( detail, holes );

const material1 = new THREE.MeshBasicMaterial( { side: THREE.DoubleSide, color: 0x000000, wireframe: true, transparent: true, opacity: 0.99 } );
const mesh1 = new THREE.Mesh( g, material1 );
scene.add( mesh1 );
const material2 = new THREE.MeshBasicMaterial( { side: THREE.FrontSide, color: 0x006600, transparent: true, opacity: 0.9 } );
const mesh2 = new THREE.Mesh( g, material2 );
scene.add( mesh2 );

 ``` 
---

.................................................................... Triangulation of Implicit Surfaces ..............................................................................

Algorithm modified.

#### EXAMPLE

genus2.png
![genus2.png](https://github.com/hofk/THREEi.js/blob/master/genus2.png)

