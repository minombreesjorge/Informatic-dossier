<template>
  <footer class="footer">
    <div class="footer-bottom">
      <p>&copy; {{ currentYear }} Carrera de Informática. Todos los derechos reservados.</p>
    </div>
  </footer>
</template>

<script setup>
import { ref } from 'vue';

const currentYear = ref(new Date().getFullYear());
</script>

<style scoped>
.footer {
  background-color: transparent;
  color: #8892b0;
  padding: 4rem 2rem 2rem;
  font-family: 'Inter', sans-serif;
}

.footer-bottom {
  margin-top: 2rem;
  text-align: center;
  font-size: 0.9rem;
  color: #8892b0;
  border-top: 1px solid #1d2d50;
  padding-top: 2rem;
}
</style>
