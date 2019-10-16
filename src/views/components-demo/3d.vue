<template>
  <div ref="info" />
</template>

<script>
import * as THREE from 'THREE'
export default {
  name: 'Animation',
  data() {
    return {
      camera: '',
      mesh: '',
      scene: '',
      renderer: ''
    }
  },
  mounted() {
    this.init()
    this.animate()
  },
  methods: {
    init() {
      this.scene = new THREE.Scene()
      this.scene.background = new THREE.Color(0xffffff)
      this.camera = new THREE.PerspectiveCamera(
        60,
        window.innerWidth / window.innerHeight,
        1,
        15000
      )
      this.camera.position.z = 5000
      const geometry = new THREE.BoxBufferGeometry(100, 100, 100)
      const material = new THREE.MeshNormalMaterial()
      this.mesh = new THREE.Mesh(geometry, material)
      this.scene.add(this.mesh)
      const num = 50
      let object
      let parent = this.mesh
      for (let i = 0; i < num; i++) {
        object = new THREE.Mesh(geometry, material)
        object.position.x = 100
        parent.add(object)
        parent = object
      }
      parent = this.mesh
      for (let i = 0; i < num; i++) {
        object = new THREE.Mesh(geometry, material)
        object.position.x = -100
        parent.add(object)
        parent = object
      }
      parent = this.mesh
      for (let i = 0; i < num; i++) {
        object = new THREE.Mesh(geometry, material)
        object.position.y = 100
        parent.add(object)
        parent = object
      }
      parent = this.mesh
      for (let i = 0; i < num; i++) {
        object = new THREE.Mesh(geometry, material)
        object.position.y = -100
        parent.add(object)
        parent = object
      }
      parent = this.mesh
      for (let i = 0; i < num; i++) {
        object = new THREE.Mesh(geometry, material)
        object.position.z = 100
        parent.add(object)
        parent = object
      }
      parent = this.mesh
      for (let i = 0; i < num; i++) {
        object = new THREE.Mesh(geometry, material)
        object.position.z = -100
        parent.add(object)
        parent = object
      }
      this.renderer = new THREE.WebGLRenderer({ antialias: true })
      this.renderer.setSize(window.innerWidth - 220, window.innerHeight - 120)
      this.renderer.setPixelRatio(window.devicePixelRatio)
      this.$refs.info.appendChild(this.renderer.domElement)
    },
    render() {
      var time = Date.now() * 0.001
      var rx = Math.sin(time * 0.5) * 0.125
      var ry = Math.sin(time * 0.5) * 0.125
      var rz = Math.sin(time * 0.6) * 0.125
      // this.camera.position.x +=  this.camera.position.x  * 0.05;
      // this.camera.position.y +=  this.camera.position.y  * 0.05;
      // this.camera.lookAt( this.scene.position );
      this.mesh.traverse(function(object) {
        object.rotation.x = rx
        object.rotation.y = ry
        object.rotation.z = rz
      })
      this.renderer.render(this.scene, this.camera)
    },
    animate() {
      requestAnimationFrame(this.animate)
      this.render()
    }
  }
}
</script>

<style scoped>
canvas {
  display: block;
}
body {
  margin: 0;
  padding: 0;
}
#info {
  position: absolute;
  top: 0px;
  width: 100%;
  box-sizing: border-box;
  text-align: center;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
  z-index: 1; /* TODO Solve this in HTML */
}

.dg.ac {
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
  z-index: 2 !important; /* TODO Solve this in HTML */
}
</style>
