<template>
  <section class="ethics-section">
    <div class="code-window" ref="codeWindow">
      <div class="window-header">
        <div class="controls">
          <span class="dot red"></span>
          <span class="dot yellow"></span>
          <span class="dot green"></span>
        </div>
        <div class="tab">ethics.js</div>
      </div>
      
      <div class="code-content">
        <div class="line-numbers">
          <span v-for="n in lineCount" :key="n">{{ n }}</span>
        </div>

        <div class="code-block">
          <div class="code-line comment">// Código de Ética</div>
          <div class="code-line">const ethicsPrinciples = {</div>
          <div class="principles">
            <div class="principle" v-for="(value, key, index) in principles" :key="key">
              <span class="property">{{ key }}</span>: 
              <span class="string">'{{ value }}'</span>{{ index === Object.keys(principles).length - 1 ? '' : ',' }}
            </div>
          </div>
          <div class="code-line">}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const principles = {
  responsabilidad: 'Asumir las consecuencias de nuestras acciones y decisiones tecnológicas',
  privacidad: 'Respetar y proteger la información personal de los usuarios',
  transparencia: 'Ser claros sobre el funcionamiento y las limitaciones de nuestros sistemas',
  equidad: 'Asegurar que nuestras soluciones no discriminen ni generen sesgos injustos',
  seguridad: 'Implementar medidas robustas para proteger los sistemas y datos'
}

const lineCount = computed(() => {
  return Object.keys(principles).length + 3 
})

const codeWindow = ref(null)

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
        observer.unobserve(entry.target)
      }
    })
  }, { threshold: 0.1 }) 

  if (codeWindow.value) {
    observer.observe(codeWindow.value)
  }
})
</script>

<style scoped>
.ethics-section {
  min-height: 100vh;
  background-color: transparent;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  font-family: 'Menlo', Monaco, 'Courier New', monospace;
}

.code-window {
  width: 90%;
  max-width: 1400px;
  background-color: #1E1E1E;
  border-radius: 16px;
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.6);
  opacity: 0;
  transform: translateY(50px);
  transition: opacity 0.8s ease-out, transform 0.8s ease-out;
}

.code-window.visible {
  opacity: 1;
  transform: translateY(0);
}

.window-header {
  background-color: #2D2D2D;
  padding: 1.2rem 1.8rem;
  border-radius: 16px 16px 0 0;
  display: flex;
  align-items: center;
}

.controls {
  display: flex;
  gap: 1rem;
}

.dot {
  width: 20px;
  height: 20px;
  border-radius: 50%;
}

.red { background-color: #ff5f56; }
.yellow { background-color: #ffbd2e; }
.green { background-color: #27c93f; }

.tab {
  margin-left: 2rem;
  color: #fff;
  font-size: 1.3rem;
  padding: 0.4rem 1.2rem;
  background-color: #1E1E1E;
  border-radius: 8px;
}

.code-content {
  padding: 2.5rem;
  display: flex;
  gap: 2.5rem;
  overflow-x: auto;
}

.line-numbers {
  display: flex;
  flex-direction: column;
  color: #858585;
  user-select: none;
  padding-right: 2rem;
  border-right: 2px solid #404040;
  text-align: right;
  font-size: 1.3rem;
}

.line-numbers span {
  line-height: 2;
  min-height: 2em;
  opacity: 0;
  transform: translateX(-20px);
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}

.code-window.visible .line-numbers span {
  opacity: 1;
  transform: translateX(0);
}

.code-block {
  flex: 1;
  font-size: 1.3rem;
}

.code-line {
  color: #fff;
  line-height: 2;
  min-height: 2em;
  opacity: 0;
  transform: translateX(20px);
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}

.code-window.visible .code-line {
  opacity: 1;
  transform: translateX(0);
}

.comment {
  color: #6A9955;
}

.principles {
  padding-left: 3rem;
}

.principle {
  line-height: 2;
  min-height: 2em;
  opacity: 0;
  transform: translateX(20px);
  transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}

.code-window.visible .principle {
  opacity: 1;
  transform: translateX(0);
}

.property {
  color: #9CDCFE;
}

.string {
  color: #CE9178;
}

.code-window:hover {
  transform: translateY(-5px);
  transition: transform 0.3s ease;
  box-shadow: 0 35px 70px rgba(0, 0, 0, 0.7);
}

/* Responsive styles */
@media (max-width: 1400px) {
  .code-window {
    width: 95%;
    font-size: 1.2rem;
  }
  
  .principles {
    padding-left: 2.5rem;
  }
}

@media (max-width: 1200px) {
  .code-window {
    font-size: 1.1rem;
  }
  
  .principles {
    padding-left: 2rem;
  }
  
  .code-content {
    padding: 2rem;
    gap: 2rem;
  }
  
  .tab {
    font-size: 1.1rem;
  }
  
  .dot {
    width: 16px;
    height: 16px;
  }
}

@media (max-width: 992px) {
  .code-window {
    font-size: 1rem;
  }
  
  .principles {
    padding-left: 1.5rem;
  }
  
  .code-content {
    padding: 1.5rem;
    gap: 1.5rem;
  }
  
  .tab {
    font-size: 1rem;
    padding: 0.3rem 1rem;
  }
  
  .window-header {
    padding: 1rem 1.5rem;
  }
}

@media (max-width: 768px) {
  .ethics-section {
    padding: 1rem;
  }
  
  .code-window {
    font-size: 0.9rem;
  }
  
  .principles {
    padding-left: 1rem;
  }
  
  .code-content {
    padding: 1rem;
    gap: 1rem;
  }
  
  .line-numbers {
    padding-right: 1rem;
  }
  
  .tab {
    font-size: 0.9rem;
    padding: 0.2rem 0.8rem;
  }
  
  .window-header {
    padding: 0.8rem 1rem;
  }
  
  .dot {
    width: 12px;
    height: 12px;
  }
}

@media (max-width: 576px) {
  .code-window {
    font-size: 0.8rem;
  }
  
  .principles {
    padding-left: 0.5rem;
  }
  .code-block{
    font-size: 0.9rem;
  }
  
  .code-content {
    padding: 0.8rem;
    gap: 0.8rem;
  }
  
  .line-numbers {
    padding-right: 0.9rem;
  }
  
  .tab {
    font-size: 0.8rem;
    padding: 0.2rem 0.6rem;
    margin-left: 1rem;
  }
  
  .window-header {
    padding: 0.6rem 0.8rem;
  }
  
  .dot {
    width: 10px;
    height: 10px;
  }
}

/* Staggered animation delays */
.code-window.visible .line-numbers span:nth-child(1),
.code-window.visible .code-line:nth-child(1) { transition-delay: 0.1s; }
.code-window.visible .line-numbers span:nth-child(2),
.code-window.visible .code-line:nth-child(2) { transition-delay: 0.2s; }
.code-window.visible .principle:nth-child(1) { transition-delay: 0.3s; }
.code-window.visible .principle:nth-child(2) { transition-delay: 0.4s; }
.code-window.visible .principle:nth-child(3) { transition-delay: 0.5s; }
.code-window.visible .principle:nth-child(4) { transition-delay: 0.6s; }
.code-window.visible .principle:nth-child(5) { transition-delay: 0.7s; }
.code-window.visible .line-numbers span:last-child,
.code-window.visible .code-line:last-child { transition-delay: 0.8s; }
</style>