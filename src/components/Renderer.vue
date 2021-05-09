<template></template>

<script lang="ts">
import { ref, defineComponent } from "vue";
import * as THREE from "three";
import { STLLoader } from "three/examples/jsm/loaders/STLLoader";
import {
  BoxGeometry,
  Mesh,
  MeshBasicMaterial,
  PerspectiveCamera,
  Scene,
  WebGLRenderer,
} from "three";

export default defineComponent({
  name: "Renderer",
  props: {},
  setup: (): void => {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    const geometry = new THREE.BoxGeometry();
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new THREE.Mesh(geometry, material);

    camera.position.set(0,10,0);
    const cameraTarget = new THREE.Vector3(0, -0.25, 0);
    // scene.add(cube);

    scene.background = new THREE.Color(0xf9f9f9);
    // scene.fog = new THREE.Fog(0x72645b, 2, 15);

    // Ground
    const plane = new THREE.Mesh(
      new THREE.PlaneGeometry(25, 25, 10, 10),
      new THREE.MeshBasicMaterial({ color: 0xf9f9f9, wireframe: false })
    );
    plane.rotation.x = -Math.PI / 2;
    plane.position.y = -0.5;
    scene.add(plane);
    plane.receiveShadow = true;

    const loader = new STLLoader();
    loader.load("../../test.stl", function (geometry) {
      const material = new THREE.MeshPhongMaterial({
        color: 0x00ff00,
        // specular: 0x111111,
        // shininess: 200,
      });
      const mesh = new THREE.Mesh(geometry, material);

      mesh.position.set(0, 5, 0);
      mesh.rotation.set(0, -Math.PI / 2, 0);
      mesh.scale.set(0.5, 0.5, 0.5);
      mesh.castShadow = true;
      mesh.receiveShadow = true;

      scene.add(mesh);
    });

    function animate() {
      requestAnimationFrame(animate);

      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
      render();
      // renderer.render(scene, camera);
    }

    function render() {
      const timer = Date.now() * 0.0005;
      camera.position.x = Math.cos(timer) * 10;
      camera.position.z = Math.sin(timer) * 10;
      camera.lookAt(cameraTarget);
      renderer.render(scene, camera);
    }

    animate();
  },
});
</script>

<style scoped lang="scss">
@import "../styles/_variables.scss";
</style>
