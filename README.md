# TaskHub

Aplicacion web de gestion de tareas desarrollada con Vue 3 y Vite.
Permite crear, filtrar, completar y eliminar tareas, mostrando estadisticas
actualizadas en tiempo real mediante contadores animados.

## Demo

[Ver aplicacion en vivo](https://mi-app-tasks.vercel.app/)

## Funcionalidades

- Agregar nuevas tareas.
- Eliminar tareas existentes.
- Marcar tareas como completadas o pendientes.
- Filtrar tareas por estado: Todas, Pendientes y Completadas.
- Visualizar estadisticas en tiempo real.
- Contadores animados con CountUp.js.
- Interfaz responsiva.

## Tecnologias utilizadas

- Vue 3
- Vite
- JavaScript
- HTML5
- CSS3
- Vue Router
- Font Awesome
- CountUp.js
- Vercel

## Instalacion local

```bash
npm install
npm run dev
```

Luego abre la URL mostrada en la terminal, normalmente:

```bash
http://localhost:5173
```

## Scripts disponibles

```bash
npm run dev
```

Inicia el servidor de desarrollo.

```bash
npm run build
```

Genera la version de produccion.

```bash
npm run preview
```

Previsualiza la version generada para produccion.

```bash
npm run lint
```

Ejecuta ESLint y corrige errores cuando sea posible.

## Estructura principal

```txt
src/
+-- assets/
+-- components/
+-- router/
+-- views/
+-- App.vue
`-- main.js
```

## Aprendizajes

Este proyecto permitio practicar:

- Manejo de estado local en Vue.
- Uso de propiedades computadas.
- Renderizado dinamico de listas.
- Filtrado de informacion segun estado.
- Organizacion de una aplicacion mediante componentes.
- Integracion de librerias externas.

## Posibles mejoras

- Separar el componente principal en componentes mas pequenos para mejorar la mantenibilidad del proyecto.
- Evitar tareas vacias.
- Guardar las tareas en localStorage.
- Agregar edicion de tareas.
- Mejorar accesibilidad en botones e iconos.
- Agregar pruebas basicas para la logica de tareas.

## Autora

**Hazel Chavez Alvarado**  
[Portafolio](https://portafolio-hazel-chavez.vercel.app/) | [LinkedIn](https://www.linkedin.com/in/hazel-chavez-alvarado/)
