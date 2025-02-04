<template>
  <div class="app">
    <div class="hero-section">
      <Hero />
    </div>
    
    <div class="content-wrapper">
      <Informatica />
      
      <div class="decorative-section">
        <img src="./components/brain.png" alt="" class="decorative-element brain" />
        <img src="./components/security.png" alt="" class="decorative-element security" />
        <Desafios />
      </div>
      
      <CodigoEtica />
      
      <div class="decorative-section">
        <img src="./components/cloud.png" alt="" class="decorative-element cloud" />
        <img src="./components/router.png" alt="" class="decorative-element router" />
        <CamposLaborales />
      </div>
      
      <pie />
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import Hero from './components/Hero.vue'
import Informatica from './components/Informatica.vue'
import Desafios from './components/Desafios.vue'
import CodigoEtica from './components/CodigoEtica.vue'
import CamposLaborales from './components/CamposLaborales.vue'
import pie from './components/footer.vue'

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
      } else {
        entry.target.classList.remove('visible')
      }
    })
  }, {
    threshold: 0.1,
    rootMargin: '0px 0px -100px 0px'
  })

  document.querySelectorAll('.decorative-element').forEach(el => {
    observer.observe(el)
  })
})
</script>

<style>
:root {
  --color-base: #0a192f;
  --color-acento-1: #00ff88;
  --color-acento-2: #00f7ff;
  --color-texto: #ccd6f6;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: var(--color-base);
  color: var(--color-texto);
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}

.app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.content-wrapper {
  position: relative;
}

.decorative-section {
  position: relative;
  margin-bottom: 60px;
}

.decorative-element {
  position: absolute;
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 1s ease, transform 1s ease;
  width: 80px;
  height: auto;
  z-index: 1;
}

.brain {
  top: -50px;
  left: -90px;
  width: 170px;
  height: 160px;
}

.security {
  top: 550px;
  right: -200px;
  width: 250px;
  height: 250px;
}

.cloud {
  top: -50px;
  left: -30px;
  width: 180px;
}

.router {
  bottom: -40px;
  right: -115px;
  width: 150px;
  height: 140px;
}

.decorative-element.visible {
  opacity: 1;
  transform: translateY(0);
}

@keyframes float {
  0%, 100% {
    transform: translateY(0) rotate(0deg);
  }
  25% {
    transform: translateY(-10px) rotate(2deg);
  }
  75% {
    transform: translateY(5px) rotate(-2deg);
  }
}

.decorative-element.visible {
  animation: float 8s ease-in-out infinite;
}

h1, h2, h3 {
  margin-bottom: 20px;
}

.seccion {
  margin-bottom: 60px;
  position: relative;
  z-index: 2;
}

.btn {
  background-color: var(--color-acento-1);
  color: var(--color-base);
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn:hover {
  background-color: var(--color-acento-2);
  box-shadow: 0 0 10px var(--color-acento-2);
}

.tarjeta {
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  padding: 20px;
  transition: all 0.3s ease;
}

.tarjeta:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 247, 255, 0.3);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.fade-in {
  animation: fadeIn 0.5s ease-out forwards;
}

@media (max-width: 768px) {
  .decorative-element {
    width: 60px; 
  }
  

  .brain, .globe {
    left: -20px;
  }
  
  .security, .laptop, .router {
    right: -20px;
  }
}
</style>
