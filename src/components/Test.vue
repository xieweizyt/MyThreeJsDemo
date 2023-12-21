<template>
  <div></div>
</template>

<script setup>
import * as three from "three";
import { OrbitControls } from "three/addons/controls/OrbitControls.js";

// 创建场景
const scene = new three.Scene();

// 创建相机 参数：视角/宽高比/近平面/远平面
const camera = new three.PerspectiveCamera(
  45,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);

// 创建渲染器
const renderer = new three.WebGL1Renderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

// 创建几何体
const geometry = new three.BoxGeometry(1, 1, 1);

// 创建材质
const material = new three.MeshBasicMaterial({ color: 0x00ff00 });

// 创建网格
const cube = new three.Mesh(geometry, material);

// 网格添加到场景
scene.add(cube);

// 设置相机位置
camera.position.x = 5;
camera.position.y = 5;
camera.position.z = 5;
camera.lookAt(0, 0, 0);

// 添加世界坐标系
const axesHelper = new three.AxesHelper(5);
scene.add(axesHelper);

// 轨道控制器
const controls = new OrbitControls(camera, renderer.domElement);
// 阻尼惯性
controls.enableDamping = true;

// controls.update();
// renderer.render(scene, camera);

// 渲染函数
function animate() {
  requestAnimationFrame(animate);
  //旋转
  // cube.rotation.x += 0.01;
  // cube.rotation.y += 0.01;
  controls.update();
  //渲染
  renderer.render(scene, camera);
}
animate();
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
.canvas {
  top: 0;
  left: 0;
  right: 0;
  widows: 100%;
  height: 100vh;
}
</style>
