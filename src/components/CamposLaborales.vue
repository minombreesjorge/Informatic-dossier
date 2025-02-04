<template>
  <section class="campos-laborales" ref="sectionRef" :class="{ 'visible': isVisible }">
    <h2 class="title">Campos Laborales</h2>
    <div class="filtros">
      <button 
        v-for="categoria in categorias" 
        :key="categoria" 
        @click="filtrarPor(categoria)" 
        :class="{ 'activo': categoriaActual === categoria }"
        class="btn-filtro"
      >
        {{ categoria }}
      </button>
    </div>
    <transition-group name="campo-list" tag="div" class="campos-grid">
      <div 
        v-for="(campo, index) in camposFiltrados" 
        :key="campo.titulo" 
        class="campo-tarjeta"
        :ref="el => { if (el) campoRefs[index] = el }"
        :class="{ 'visible': campoVisible[index] }"
        @mouseenter="rotarTarjeta"
        @mouseleave="resetearTarjeta"
      >
        <div class="campo-contenido">
          <div class="campo-icono">
            <component :is="campo.icono" size="35" stroke-width="1.5" />
          </div>
          <h3 class="campo-titulo">{{ campo.titulo }}</h3>
          <p class="campo-descripcion">{{ campo.descripcion }}</p>
        </div>
      </div>
    </transition-group>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, watch, nextTick } from 'vue'
import { 
  Globe, Shield, BarChart, Brain, Smartphone, Cloud, Wifi, Blocks
} from 'lucide-vue-next'

const categorias = ['Todos', 'Desarrollo', 'Seguridad', 'Datos', 'IA']
const categoriaActual = ref('Todos')

const campos = ref([
  { titulo: 'Desarrollo Web', descripcion: 'Creación de sitios y aplicaciones web', categoria: 'Desarrollo', icono: Globe },
  { titulo: 'Ciberseguridad', descripcion: 'Protección de sistemas y redes', categoria: 'Seguridad', icono: Shield },
  { titulo: 'Ciencia de Datos', descripcion: 'Análisis y visualización de datos', categoria: 'Datos', icono: BarChart },
  { titulo: 'Inteligencia Artificial', descripcion: 'Desarrollo de sistemas inteligentes', categoria: 'IA', icono: Brain },
  { titulo: 'Desarrollo Móvil', descripcion: 'Creación de apps para dispositivos móviles', categoria: 'Desarrollo', icono: Smartphone },
  { titulo: 'Cloud Computing', descripcion: 'Gestión de servicios en la nube', categoria: 'Desarrollo', icono: Cloud },
  { titulo: 'IoT', descripcion: 'Internet de las cosas y dispositivos conectados', categoria: 'Desarrollo', icono: Wifi },
  { titulo: 'Blockchain', descripcion: 'Desarrollo de tecnologías descentralizadas', categoria: 'Seguridad', icono: Blocks }
])

const camposFiltrados = computed(() => {
  if (categoriaActual.value === 'Todos') {
    return campos.value
  }
  return campos.value.filter(campo => campo.categoria === categoriaActual.value)
})

const campoRefs = ref([])
const campoVisible = ref([])

function filtrarPor(categoria) {
  categoriaActual.value = categoria
}

function rotarTarjeta(event) {
  const tarjeta = event.currentTarget
  const rect = tarjeta.getBoundingClientRect()
  const x = event.clientX - rect.left
  const y = event.clientY - rect.top
  tarjeta.style.transform = `perspective(1000px) rotateX(${(y - rect.height / 2) / 20}deg) rotateY(${-(x - rect.width / 2) / 20}deg) scale(1.05)`
}

function resetearTarjeta(event) {
  event.currentTarget.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) scale(1)'
}

const sectionRef = ref(null)
const isVisible = ref(false)

onMounted(() => {
  const sectionObserver = new IntersectionObserver((entries) => {
    if (entries[0].isIntersecting) {
      isVisible.value = true
      sectionObserver.disconnect()
    }
  }, { threshold: 0.2 })

  if (sectionRef.value) {
    sectionObserver.observe(sectionRef.value)
  }

  const cardObserver = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const index = campoRefs.value.findIndex(ref => ref === entry.target)
        if (index !== -1) {
          campoVisible.value[index] = true
        }
      }
    })
  }, { threshold: 0.1 })

  campoRefs.value.forEach(ref => {
    if (ref) cardObserver.observe(ref)
  })
})

watch(camposFiltrados, () => {
  campoVisible.value = new Array(camposFiltrados.value.length).fill(false)
  nextTick(() => {
    campoRefs.value.forEach((ref, index) => {
      if (ref && ref.getBoundingClientRect().top < window.innerHeight) {
        campoVisible.value[index] = true
      }
    })
  })
})
</script>

<style scoped>
.campos-laborales {
  padding: 1.1rem;
  background: transparent;
  color: #fff;
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 1s ease, transform 1s ease;
}

.campos-laborales.visible {
  opacity: 1;
  transform: translateY(0);
}

.title {
  text-align: center;
  margin-bottom: 2rem;
  font-size: 2.5rem;
}

.filtros {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1rem;
  margin-bottom: 3rem;
}

.btn-filtro {
  padding: 0.5rem 1rem;
  background: transparent;
  border: 2px solid #8892b0;
  color: #8892b0;
  cursor: pointer;
  border-radius: 2rem;
  font-weight: bold;
  transition: all 0.3s ease;
}

.btn-filtro:hover, .btn-filtro.activo {
  transform: scale(1.05);
  background: #8892b0;
  color: #fff;
}

.campos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.campo-tarjeta {
  background: transparent;
  border: 2px solid #8892b0;
  border-radius: 1rem;
  overflow: hidden;
  transition: all 0.3s ease;
  opacity: 0;
  transform: translateY(30px);
}

.campo-tarjeta.visible {
  opacity: 1;
  transform: translateY(0);
}

.campo-contenido {
  padding: 1rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.campo-icono {
  font-size: 2rem;
  margin-top: 0.1;
  margin-bottom: 1rem;
  color: #8892b0;
}

.campo-titulo {
  font-size: 1.25rem;
  margin: 0.1rem;
  color: #fff;
}

.campo-descripcion {
  font-size: 0.9rem;
  color: #ccc;
  text-align: center;
}

.campo-tarjeta {
  transition: all 1s ease;
  opacity: 0;
  transform: translateY(30px);
}
.campo-tarjeta.visible {
  opacity: 1;
  transform: translateY(0);
}


</style>