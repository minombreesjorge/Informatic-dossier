# Informatic-dossier

Este proyecto es una landing page sobre la informática, desarrollada principalmente con Vue 3 y Vite. A continuación, se explican los pasos para configurar y trabajar con este proyecto.

## Requisitos Previos

Antes de comenzar, asegúrate de tener instalado lo siguiente en tu sistema:

- [Node.js](https://nodejs.org/) (versión recomendada: 18.x o superior)
- [Git](https://git-scm.com/) (para clonar el repositorio si es necesario)
- [VSCode](https://code.visualstudio.com/) (opcional, pero recomendado)
  - Extensión recomendada: [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar)
  - Deshabilita Vetur si está activado para evitar conflictos

## Instalación y Configuración

Sigue estos pasos para instalar y ejecutar el proyecto en tu entorno local.

### 1. Clonar el Repositorio

Si aún no tienes el código, clónalo con Git:

```sh
git clone https://github.com/usuario/informatic-dossier.git
cd informatic-dossier
```

### 2. Instalar Dependencias

Ejecuta el siguiente comando para instalar todas las dependencias necesarias:

```sh
npm install
```

### 3. Iniciar el Servidor de Desarrollo

Para ejecutar el proyecto en modo de desarrollo y ver los cambios en tiempo real, usa:

```sh
npm run dev
```

Esto iniciará un servidor local, normalmente accesible en `http://localhost:5173/`.

### 4. Estructura del Proyecto

El proyecto sigue una estructura estándar de Vue 3 con Vite:

- **`src/`**: Código fuente del proyecto (componentes, estilos, lógica principal).
- **`src/components/`**: Componentes reutilizables de Vue.
- **`public/`**: Archivos estáticos como imágenes y favicons.
- **`package.json`**: Contiene las dependencias del proyecto y los scripts disponibles.
- **`vite.config.js`**: Configuración de Vite.

### 5. Construir el Proyecto para Producción

Cuando el proyecto esté listo para su despliegue, genera una versión optimizada con:

```sh
npm run build
```

Esto creará una carpeta `dist/` con los archivos listos para subir a un servidor o plataforma de hosting.

### 6. Vista Previa del Proyecto Construido

Para verificar cómo se verá el proyecto en producción antes de subirlo, puedes ejecutar:

```sh
npm run preview
```

Esto iniciará un servidor local con la versión optimizada del proyecto.

## Contribución

Si deseas contribuir al proyecto:
1. Haz un fork del repositorio.
2. Crea una nueva rama (`git checkout -b nueva-funcionalidad`).
3. Realiza tus cambios y haz un commit (`git commit -m "Añadir nueva funcionalidad"`).
4. Envía un pull request.
