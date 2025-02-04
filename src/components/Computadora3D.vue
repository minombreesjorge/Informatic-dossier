<template>
    <div ref="container" class="three-container"></div>
  </template>
  
  <script setup>
  import { ref, onMounted, onUnmounted } from 'vue';
  import * as THREE from 'three';
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
  
  const container = ref(null);
  let scene, camera, renderer, controls, laptopGroup, pointLight;
  
  const initScene = () => {
    scene = new THREE.Scene();
    scene.background = new THREE.Color(0x1a1a1a);
    
    camera = new THREE.PerspectiveCamera(75, container.value.clientWidth / container.value.clientHeight, 0.1, 1000);
    camera.position.set(0, 1, 2);
  
    renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    renderer.setSize(container.value.clientWidth, container.value.clientHeight);
    renderer.setPixelRatio(window.devicePixelRatio);
    container.value.appendChild(renderer.domElement);
  
    controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.enableZoom = true;
    controls.autoRotate = true;
    controls.autoRotateSpeed = 1.5;
  
    addLighting();
    addLaptop();
    animate();
    window.addEventListener('resize', handleResize);
    container.value.addEventListener('mousemove', onMouseMove);
  };
  
  const addLighting = () => {
    scene.add(new THREE.AmbientLight(0xffffff, 0.3));
    
    const spotLight = new THREE.SpotLight(0xffffff, 1.5);
    spotLight.position.set(3, 5, 3);
    spotLight.castShadow = true;
    scene.add(spotLight);
    
    pointLight = new THREE.PointLight(0x64ffda, 1.2, 100);
    scene.add(pointLight);
  };
  
  const addLaptop = () => {
    laptopGroup = new THREE.Group();
  
    const materialConfig = (color, metalness = 0.9, roughness = 0.1) => 
      new THREE.MeshPhysicalMaterial({ color, metalness, roughness, envMapIntensity: 0.8 });
  
    const baseMesh = new THREE.Mesh(new THREE.BoxGeometry(1.6, 0.05, 1.1), materialConfig(0x212121));
    baseMesh.castShadow = true;
    baseMesh.receiveShadow = true;
    laptopGroup.add(baseMesh);
  
    const screenMesh = new THREE.Mesh(new THREE.BoxGeometry(1.5, 0.85, 0.03), materialConfig(0x000000, 0.3, 0.7));
    screenMesh.position.set(0, 0.45, -0.52);
    laptopGroup.add(screenMesh);
  
    const frameMesh = new THREE.Mesh(new THREE.BoxGeometry(1.55, 0.9, 0.05), materialConfig(0x404040));
    frameMesh.position.set(0, 0.45, -0.55);
    laptopGroup.add(frameMesh);
  
    const keyboardTexture = new THREE.TextureLoader().load('https://i.imgur.com/Iq5Fh8j.png');
    const keyboardMesh = new THREE.Mesh(new THREE.PlaneGeometry(1.4, 0.75), new THREE.MeshBasicMaterial({ map: keyboardTexture, transparent: true }));
    keyboardMesh.rotation.x = -Math.PI / 2;
    keyboardMesh.position.set(0, 0.025, 0.3);
    laptopGroup.add(keyboardMesh);
    
    scene.add(laptopGroup);
  };
  
  const animate = () => {
    requestAnimationFrame(animate);
    controls.update();
    renderer.render(scene, camera);
  };
  
  const handleResize = () => {
    if (container.value) {
      camera.aspect = container.value.clientWidth / container.value.clientHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(container.value.clientWidth, container.value.clientHeight);
    }
  };
  
  const onMouseMove = (event) => {
    const rect = container.value.getBoundingClientRect();
    const mouse = new THREE.Vector2(
      ((event.clientX - rect.left) / rect.width) * 2 - 1,
      -((event.clientY - rect.top) / rect.height) * 2 + 1
    );
  
    const raycaster = new THREE.Raycaster();
    raycaster.setFromCamera(mouse, camera);
    const intersects = raycaster.intersectObject(laptopGroup, true);
  
    if (intersects.length > 0) {
      pointLight.position.copy(intersects[0].point);
    }
  };
  
  onMounted(initScene);
  
  onUnmounted(() => {
    window.removeEventListener('resize', handleResize);
    container.value.removeEventListener('mousemove', onMouseMove);
    controls.dispose();
    renderer.dispose();
  });
  </script>
  
  <style>
  .three-container {
    width: 100%;
    height: 100%;
  }
  </style>