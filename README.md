# tf<!DOCTYPE html>
<html lang="en"><head>
<title>three.js webgl Geometrik figures</title>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
<link type="text/css" rel="stylesheet" href="https://threejs.org/examples/main.css">
</head>
<body>
<div id="info">
Trehmernye figury

</div>

<script type="module">

import * as THREE from 'https://threejs.org/build/three.module.js';

import { OrbitControls } from 'https://threejs.org/examples/jsm/controls/OrbitControls.js';

var camera, scene, renderer;
var controls;
var ambientLight, light;
init();
animate();

function init() {

var container = document.createElement( 'div' );
document.body.appendChild( container );

// CAMERA
camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 1, 90000 );
camera.position.set( 150, 100, 100 );

// LIGHTS
ambientLight = new THREE.AmbientLight( 0xF08080 ); // 0.2

light = new THREE.DirectionalLight( 0xF08080, 1.0 );
light.position.set( 1, 1, 1 );
// direction is set in GUI

// RENDERER
renderer = new THREE.WebGLRenderer( { antialias: true } );
renderer.setPixelRatio( window.devicePixelRatio );
renderer.setSize( window.innerWidth, window.innerHeight );
container.appendChild( renderer.domElement );

// EVENTS
window.addEventListener( 'resize', onWindowResize, false );

// CONTROLS
controls = new OrbitControls( camera, renderer.domElement );
controls.addEventListener( 'change', render );
//controls.rotateSpeed = 1;
controls.enableZoom = true;
controls.zoomSpeed = 0.5;

controls.minDistance = 50;
controls.maxDistance = 2500;

controls.enableDamping = true;

// scene itself
scene = new THREE.Scene();
scene.background = new THREE.Color( 0xF08080 );

scene.add( ambientLight );
scene.add( light );

var textureLoader = new THREE.TextureLoader();
var texture = textureLoader.load( 'mramor.jpg' );
texture.wrapS = texture.wrapT = THREE.RepeatWrapping;
texture.repeat.set( 2, 2 );

var material = new THREE.MeshPhongMaterial( {
map: texture,
bumpMap: texture,
shininess: 3,
side: THREE.DoubleSide
} );

var points = [ ];
for ( var i = - 1.0; i < 0.7; i = i + 0.1 ) {
points.push( new THREE.Vector2( 5 + 32*Math.exp( -i*i ), -24*i ) );
}

var geometry = new THREE.LatheGeometry( points, 32 );
var object = new THREE.Mesh( geometry, material );
scene.add( object );

var texture = textureLoader.load( 'mramor.jpg' );
texture.wrapS = texture.wrapT = THREE.RepeatWrapping;
texture.repeat.set( 1, 1 );
var material = new THREE.MeshBasicMaterial( {
map: texture, shininess: 3 , bumpMap: texture, side: THREE.DoubleSide

} );
var geometry = new THREE.CircleGeometry( 40, 32 );
var circle = new THREE.Mesh( geometry, material );
circle.rotation.x = Math.PI/2 ;
circle.position.set( 0 , -10, 0 );
scene.add( circle );

}

// EVENT HANDLERS

function onWindowResize() {

camera.aspect = window.innerWidth / window.innerHeight;
camera.updateProjectionMatrix();

renderer.setSize( window.innerWidth, window.innerHeight );

}

//

function animate() {

requestAnimationFrame( animate );
controls.update(); //
render();

}

function render() {

renderer.render( scene, camera );

}

</script>



</body></html>
