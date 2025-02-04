<template>
  <section class="informatica-section">
    <div class="container">
      <div class="content">
        <h1 class="title" ref="title">
          ¿Qué es la Informática?
          <div class="underline"></div>
        </h1>

        <div class="grid">
          <div class="text-content">
            <p ref="paragraph1">
              La Informática es la ciencia que estudia el procesamiento automático de la información 
              mediante sistemas computacionales. Abarca el diseño, desarrollo y aplicación de software 
              y hardware para resolver problemas y optimizar procesos en diversos campos del conocimiento.
            </p>
            
            <p ref="paragraph2">
              Esta disciplina fundamental combina principios matemáticos, lógica y creatividad para 
              impulsar la innovación tecnológica. La Informática es el motor detrás de la revolución 
              digital, permitiendo avances en áreas como la inteligencia artificial, el análisis de 
              datos y la ciberseguridad.
            </p>
          </div>

          <div class="image-wrapper" ref="imageWrapper">
            <img 
              :src="'https://hebbkx1anhila5yf.public.blob.vercel-storage.com/informatica.jpg-Oyw99BDl04cziQubKcK0l3xDYuBCdm.jpeg'" 
              alt="Tecnología informática"
              class="feature-image"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const title = ref(null);
const paragraph1 = ref(null);
const paragraph2 = ref(null);
const imageWrapper = ref(null);

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

  [title.value, paragraph1.value, paragraph2.value, imageWrapper.value].forEach((el, index) => {
    if (el) {
      el.style.setProperty('--delay', `${index * 0.2}s`);
      observer.observe(el);
    }
  });
});
</script>

<style scoped>
.informatica-section {
  min-height: 100vh;
  color: #f8fafc;
  padding: 4rem 1rem;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.content {
  padding: 3rem 2rem;
}

.title {
  font-size: 2.5rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 3rem;
  color: #ccc;
  position: relative;
}

.underline {
  width: 80px;
  height: 4px;
  background: #38bdf8;
  margin: 1rem auto 0;
  border-radius: 2px;
}

.grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.text-content {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.text-content p {
  font-size: 1.125rem;
  line-height: 1.8;
  color: #cbd5e1;
}

.image-wrapper {
  border-radius: 2rem;
  overflow: hidden;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.6), 
              0 6px 6px rgba(0, 0, 0, 0.4);
  transition: transform 0.5s ease-in-out, box-shadow 0.5s ease-in-out;
}

.image-wrapper:hover {
  transform: scale(1.03); 
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.795); 
}

.feature-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.5s ease-in-out, filter 0.5s ease-in-out;
}

.image-wrapper:hover .feature-image {
  transform: scale(1.05); 
  filter: brightness(1.1); 
}

.title,
.text-content p,
.image-wrapper {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease var(--delay), transform 0.6s ease var(--delay);
}

.title.visible,
.text-content p.visible,
.image-wrapper.visible {
  opacity: 1;
  transform: translateY(0);
}

@media (max-width: 768px) {
  .informatica-section {
    padding: 2rem 1rem;
  }

  .content {
    padding: 2rem 1.5rem;
  }

  .grid {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .title {
    font-size: 2rem;
  }

  .text-content p {
    font-size: 1rem;
  }
}
</style>