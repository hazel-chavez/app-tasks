<!-- <script setup>
// --------------------------------------------------------------
// Recibimos los datos desde el componente padre (TasksPage.vue)
// Esta es la mejora principal: este componente ahora SOLO muestra,
// y ya no calcula nada por su cuenta.
// --------------------------------------------------------------
const props = defineProps({
  total: Number,
  pending: Number,
  completed: Number
})
</script>

<template>
  <header>
    <div class="header-container">

      <span class="navbar-brand mb-0 h1">

            <h1>TaskHub<img
              alt="logo"
              class="logo"
              src="@/assets/icons8-lista.png"

            /></h1>

          </span>
          <p>Gestiona tus Tareas de forma Rapida</p>
          <div class="row justify-content-center mb-5">
        <div class="col-12 col-sm-10 col-md-8 col-lg-6">
          <div class="d-flex justify-content-around stats-bar p-3 rounded-4">
            <div class="text-center container-item">
              <p class="mb-0 text-white-50">Total</p>
              <h3 class="text-white">{{ tasks.length }}</h3>
            </div>
            <div class="text-center container-item">
              <p class="mb-0 text-white-50">Pendientes</p>
              <h3 class="text-white">{{ tasks.filter(t => t.status === false).length }}</h3>
            </div>
            <div class="text-center container-item">
              <p class="mb-0 text-white-50">Completadas</p>
              <h3 class="text-white">{{ tasks.filter(t => t.status === true).length }}</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>
<style scoped>
.container-header h1 {
  font-family: Segoe UI Emoji;
  text-align: center;
  color: var(--bg-color-logo);
  font-weight: 700;
}
.container-header p{
    text-align: center;
    color: #9275f6;
    font-weight: 600;
    font-size: 20px;
}
.container-item{
  width: 25%;
    background: var(--card-bg);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 25px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1rem;
  text-align: center;
}
.container-header h1::after{
 background-image: url(@/assets/icons8-lista.png);
}
.navbar {
  display: flex;
  background-image: url(@/assets/imgHeader.jpg);
  border-radius: 15px;

}
</style> -->
