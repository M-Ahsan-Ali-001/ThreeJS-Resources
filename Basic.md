# Camera
```
const camera = new Three.PerpectiveCamera(75, innerwidth/innerHeight , 0.1 ,1000) // (angle , size ,min distance of camera , max distance of camera)

camera.position.z = 5 // change camera direction so that things are visible
                                          
```

# canvas
```
const canvas = document.getElementbyid('id-of-canvas')  as HTMLCanvasElement // last part is for angular only typscript ....

```
# Scene 

```
const scene = new Three.Scene() // create a new scene
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



#MeshMaterial
```
const meshMat =  new Three.MeshBasicMaterial(
{
// many other properties
side:Three.DoubleSide,
color:0x00FF00,
 wireframe:true,  //shows the inbuilt structure
vertexColor:true // color of every single polygone
})

```
