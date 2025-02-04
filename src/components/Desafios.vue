<template>
  <section class="desafios-eticos" ref="sectionRef">
    <h2 class="title">Desafíos Éticos</h2>
    <div class="grid-container">
      <div 
        v-for="(desafio, index) in desafios" 
        :key="index" 
        class="grid-item"
        :class="{ 'visible': visibleItems[index], [`item-${index + 1}`]: true }"
        @mouseenter="rotarTarjeta"
        @mouseleave="resetearTarjeta"
      >
        <div class="desafio-icon">
          <component :is="desafio.icon" size="35" stroke-width="1.5" />
        </div>
        <h3 class="desafio-title">{{ desafio.title }}</h3>
        <p class="desafio-description">{{ desafio.description }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, reactive } from 'vue'
import { Shield, Eye, Brain, Users, Database, Globe, Lock, Briefcase, Code, Signal, Globe2, FileText } from 'lucide-vue-next'

const desafios = [
  { icon: Shield, title: "Privacidad y Seguridad de Datos", description: "Proteger la información personal y los sistemas implica usar contraseñas seguras, cifrado de datos y controles de acceso adecuados. Además, es clave educar sobre riesgos como phishing, malware y mantener el software actualizado para prevenir amenazas cibernéticas." },
  { icon: Eye, title: "Vigilancia y Libertad", description: "Equilibrar la seguridad pública con el derecho a la privacidad y la libertad individual en la era digital." },
  { icon: Brain, title: "Inteligencia Artificial Ética", description: "Desarrollar y utilizar IA de manera responsable, evitando sesgos y garantizando la transparencia." },
  { icon: Users, title: "Inclusión y Accesibilidad", description: "Asegurar que la tecnología sea accesible y beneficiosa para todos, independientemente de sus capacidades o recursos." },
  { icon: Database, title: "Gestión de Big Data", description: "Manejar grandes volúmenes de datos de manera ética, respetando la privacidad y evitando su mal uso." },
  { icon: Globe, title: "Impacto Ambiental", description: "Reducir la huella de carbono en la tecnología implica optimizar recursos, usar energías renovables y desarrollar software eficiente y responsable. Esto minimiza el impacto ambiental y promueve prácticas sostenibles tanto en hardware como en software." },
  { icon: Lock, title: "Ciberseguridad y Delitos Informáticos", description: "Combatir el aumento de ataques cibernéticos, fraudes y la creación de software malicioso que amenaza a individuos y empresas." },
  { icon: Briefcase, title: "Impacto Laboral de la Automatización", description: "Gestionar el desplazamiento de empleos tradicionales por la automatización y fomentar la reconversión laboral." },
  { icon: Code, title: "Ética en el Desarrollo de Software", description: "Evitar prácticas de desarrollo poco éticas como el uso de dark patterns o la creación de productos adictivos." },
  { icon: Signal, title: "Desinformación y Manipulación Digital", description: "Enfrentar la propagación de fake news, deepfakes y la manipulación de información a través de algoritmos." },
];

const sectionRef = ref(null)
const visibleItems = reactive(desafios.map(() => false))

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        const index = [...sectionRef.value.querySelectorAll('.grid-item')].indexOf(entry.target)
        if (index !== -1) visibleItems[index] = true
      }
    })
  }, { threshold: 0.2 })

  sectionRef.value.querySelectorAll('.grid-item').forEach((item) => observer.observe(item))
})

function rotarTarjeta(event) {
  const tarjeta = event.currentTarget
  const rect = tarjeta.getBoundingClientRect()
  const x = event.clientX - rect.left
  const y = event.clientY - rect.top
  tarjeta.style.transform = `perspective(1000px) rotateX(${(y - rect.height / 2) / 40}deg) rotateY(${-(x - rect.width / 2) / 40}deg) scale(1.02)`
}

function resetearTarjeta(event) {
  event.currentTarget.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) scale(1)'
}
</script>

<style scoped>
.desafios-eticos {
  padding: 2rem;
  background-color: transparent;
  min-height: 80vh;
}

.title {
  color: #ccd6f6;
  font-size: 2.5rem;
  margin-bottom: 3rem;
  text-align: center;
  font-weight: bold;
  letter-spacing: 2px;
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  max-width: 1100px;
  margin: 0 auto;
}

.grid-item {
  background-color: transparent;
  padding: 1rem;
  border-radius: 15px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border: 2px solid;
  opacity: 0;
  transform: translateY(50px);
  transition: opacity 0.8s ease, transform 0.8s ease;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.grid-item.visible {
  opacity: 1;
  transform: translateY(0);
}

.item-1, .item-6, .item-11 {
  grid-column: span 2;
}

.desafio-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0.1rem;
}

.desafio-icon :deep(svg) {
  color: #8892b0;
  width: 35px;
  height: 35px;
}

.desafio-title {
  font-size: 1.25rem;
  color: #ccd6f6;
  font-weight: bold;
  margin:  0.4rem 0.1rem 0.1rem 0.1rem;
}

.desafio-description {
  font-size: 0.95rem;
  color: #ccc;
  line-height: 1.5;
  font-weight: 300;
}

/* Hover sutil */
.grid-item:hover {
  transform: perspective(1000px) rotateX(5deg) rotateY(5deg) scale(1.02);
  transition: transform 0.3s ease;
}

@media (max-width: 1024px) {
  .grid-container {
    grid-template-columns: repeat(2, 1fr);
  }

  .item-1, .item-6, .item-11 {
    grid-column: span 1; 
  }
}

/* Responsivo para móviles */
@media (max-width: 768px) {
  .grid-container {
    grid-template-columns: repeat(2, 1fr) !important; 
  }

  .section-title {
    font-size: 1.5rem !important; 
  }

  .grid-item {
    padding: 0.5rem !important; 
  }

  .desafio-title {
    font-size: 1.25rem !important; 
  }

  .desafio-description {
    font-size: 0.9rem !important; 
  }
}


</style>
