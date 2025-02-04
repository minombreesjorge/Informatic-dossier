<template>
  <section class="hero">
    <div class="hero-background">
      <div class="image-container">
        <img 
          src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/10a2f0c4221be23c238934528bab97e8.jpg-mBgb42XDuxwGyRZjB0vYDq6wT9iTyt.jpeg" 
          alt="Developer workspace" 
          class="hero-image"
        />
        <div class="image-overlay"></div>
      </div>
    </div>
    <div class="hero-content">
      <div class="content-wrapper">
        <div class="title-container">
          <span class="accent-line"></span>
          <h1 class="hero-title">Carrera de<br/>Informática</h1>
        </div>
        <p class="hero-subtitle">Diseña el futuro digital con responsabilidad</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  width: 120%; 
  height: 100vh;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  
}

.image-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.hero-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.3;
  filter: contrast(1.2) brightness(0.9) saturate(1.2);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    135deg,
    rgba(3, 3, 3, 0.95) 0%,
    rgba(3, 3, 3, 0.8) 50%,
    rgba(3, 3, 3, 0.95) 100%
  );
}

.hero-content {
  position: relative;
  z-index: 2;
  width: 100%;
  max-width: 1200px;
  padding: 0 2rem;
}

.content-wrapper {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.title-container {
  position: relative;
  padding-left: 2rem;
}

.accent-line {
  position: absolute;
  left: 0;
  top: 1rem;
  width: 4px;
  height: 70%;
  background: linear-gradient(180deg, #64FFDA 0%, rgba(100, 255, 218, 0) 100%);
}

.hero-title {
  font-size: clamp(3rem, 10vw, 5.5rem);
  font-weight: 800;
  line-height: 1.1;
  letter-spacing: -0.02em;
  color: #ffffff;
  text-transform: uppercase;
  margin: 0;
}

.hero-subtitle {
  font-size: clamp(1.1rem, 3vw, 1.5rem);
  color: #94A3B8;
  font-weight: 400;
  line-height: 1.6;
  max-width: 600px;
  margin: 0;
  letter-spacing: 0.5px;
}


@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.content-wrapper > * {
  animation: fadeIn 1s ease-out forwards;
}

.hero-title {
  animation-delay: 0.2s;
}

.hero-subtitle {
  animation-delay: 0.4s;
}



@media (max-width: 768px) {
  .hero-content {
    padding: 0 1.5rem;
  }

  .title-container {
    padding-left: 1.5rem;
  }

  .accent-line {
    width: 3px;
  }


}
</style>