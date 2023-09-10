# Camera
```
const camera = new Three.PerpectiveCamera(75, innerwidth/innerHeight , 0.1 ,1000) // (angle , size ,min distance of camera , max distance of camera)

camera.position.z = 5 // change camera direction so that things are visible
                                          
```

# Canvas
```
const canvas = document.getElementbyid('id-of-canvas')  as HTMLCanvasElement // last part is for angular only typscript ....

```
# Scene 

```
const scene = new Three.Scene() // create a new scene

scene.add(meshBox)

scene.add(light)
```

# WebGL Renderer
```
const renderer =  new Three.WebGLRenderer({
canvas = canvas // html div ....
})

renderer.setSize(innerWidth , innerHeight) // set size of the canvas 

renderer.setPixelRatio(devicePixelRatio) // prevent bluring output canvas

renderer.render(scene,camera) // start the WebGL (rendering)

```


# Geometry 
```
// There are different types of Gemoetry eg PlanGeometry
const boxGeometry = new Three.BoxGeometry(4,4,4,4) // (width : Float, height : Float, depth : Float, widthSegments : Integer, heightSegments : Integer, depthSegments : Integer) 
```



# MeshMaterial
```
// there different types of material like Phong material remember Phong need a light to be appeared
const meshMat =  new Three.MeshBasicMaterial(
{
// many other properties
side:Three.DoubleSide,
color:0x00FF00,
 wireframe:true,  //shows the inbuilt structure
vertexColor:true // color of every single polygone
})

```
# Mesh 
```
const meshBox = new Three.Mesh(boxGeometry,meshMat)
```

#  DirectionalLight

```
const light = new Three.DirectionalLight(0xFFFFFF,1) // (COLOR , intensity)
light.position.set(0,0,1) // (x,y,z)light to  the front
light.position.set(0,0,-1) // light to  the back

```

# Obital Control
```
new OrbitalControls(camera , renderer.domElement) // used to rotate the camera around the object in front of camera
```

# request for animation
```
function animate (){

requestAnimationFrame(animate); // used for animations 
Box.rotate.x += 0.01 // used to rotate the object
renderer.render(scene , camera) 

}
animate() // remember to call it otherwise it doesnot work
```
# PlaneMesh.geometry.attributes['position'].array
```
 array is a 32-bit floating point number. The array contains the X, Y, and Z coordinates for each vertex of the plane.

 const arrayAxises = PlaneMesh.geometry.attributes['position'].array

        for (let i =0 ; i<arrayAxises.length;i+=3){ // changing the shape 
            const x = arrayAxises[i]
            const y = arrayAxises[i+1]
            const z = arrayAxises[i+2]

             arrayAxises[i+2] =z + Math.random() 

        }

```

# dat.gui
```
used to tweak the values
  const datGui = new dat.GUI()
   const world = {
            plane:{

                width:10,
                height:10,
                widthSegments:500,
                heightSegments:500
            }}
  datGui.add(world.plane,'width',1,50).
        onChange(changeManager)

        datGui.add(world.plane,'height',1,50).
        onChange(changeManager) 

        datGui.add(world.plane,'widthSegments',1,500).
        onChange(changeManager)

        datGui.add(world.plane,'heightSegments',1,500).
        onChange(changeManager)



        function changeManager(){


            PlaneMesh.geometry.dispose()
            PlaneMesh.geometry = new Three.PlaneGeometry(world.plane.width,world.plane.height,world.plane.widthSegments,world.plane.heightSegments)
            const arrayAxises = PlaneMesh.geometry.attributes['position'].array
            for (let i =0 ; i<arrayAxises.length;i+=3){
                const x = arrayAxises[i]
                const y = arrayAxises[i+1]
                const z = arrayAxises[i+2]
    
                 arrayAxises[i+2] =z + Math.random() 
    
            }
        }


```

# Change Color Every vertex

```
const color:number[] =[]
const vetexCount = PlaneMesh.geometry.attributes['position'].count
for (let i=0 ;i<vetexCount; i++)
{

color.push(1,0,0)

}
const TypedArray =  new Float32Array(color)
PlaneMesh.geometry.setAttribute('color',new Three.Int8BufferAttribute(TypedArray,3))
```


# add Mouse Listenr and normalize them
```
addEventListener('mousemove',(event)=>{

mouseCord.x = (event.clientX / innerWidth) * 2 -1 

mouseCord.y = -(event.clientY / innerHeight) * 2 +1  // we do this to normalize the mouse and get right cordinate where the mouse is pointing or hovering

console.log(mouseCord)
})


```

# RayCast
```
//tells if the mouse hover over the plane
const raycaster = new Three.Raycaster()
raycaster.setFromCamera(mouseCord,camera)
const collision = raycaster.intersectObject(PlaneMesh)

if(collision.length >0)
{
    const mesh = collision[0].object as THREE.Mesh; // only of TS
    console.log(mesh.geometry);
}
}
```
