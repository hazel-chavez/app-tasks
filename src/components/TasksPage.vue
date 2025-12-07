
<template>
  <div class="container p-5">
    <header>
      <div class="container-header">
        <span class="navbar-brand mb-0 h1">
          <h1>
            TaskHub<img alt="logo" class="logo" src="@/assets/icons8-lista.png" />
          </h1>
        </span>
        <p>Gestiona tus Tareas de forma Rapida</p>
        <div class="row justify-content-center mb-5 align-items-center">
          <div class="col-12">
            <div class="d-flex flex-wrap justify-content-around stats-bar rounded-4">
              <!-- Estadísticas de tareas -->
              <div class="text-center container-item rounded-4">
                <p class="mb-0 text-white-50">Total</p>
                <h3 class="text-white">{{ tasks.length }}</h3>
              </div>
              <div class="text-center container-item rounded-4">
                <p class="mb-0 text-white-50">Pendientes</p>
                <h3 class="text-white">
                  {{ tasks.filter((t) => t.status === false).length }}
                </h3>
              </div>
              <div class="text-center container-item rounded-4">
                <p class="mb-0 text-white-50">Completadas</p>
                <h3 class="text-white">
                  {{ tasks.filter((t) => t.status === true).length }}
                </h3>
              </div>
            </div>
          </div>
        </div>
      </div>
    </header>

    <div class="container">
      <div class="row justify-content-center container-input mb-4 p-5">
        <div class="col-12 col-md-8 d-flex justify-content-center align-items-center">
          <!-- Input para agregar tarea -->
          <input
            type="text"
            class="form-control task-input me-2"
            placeholder="Agregar nueva tarea..."
            v-model="nameTasks"
            @keyup.enter="addTasks()"
          />
          <button type="button" class="btn d-flex align-items-center" v-on:click="addTasks()">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"
              class="icon icon-tabler icons-tabler-filled icon-tabler-copy-plus">
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path
                d="M18.333 6a3.667 3.667 0 0 1 3.667 3.667v8.666a3.667 3.667 0 0 1 -3.667 3.667h-8.666a3.667 3.667 0 0 1 -3.667 -3.667v-8.666a3.667 3.667 0 0 1 3.667 -3.667zm-4.333 4a1 1 0 0 0 -1 1v2h-2a1 1 0 0 0 -.993 .883l-.007 .117a1 1 0 0 0 1 1h2v2a1 1 0 0 0 .883 .993l.117 .007a1 1 0 0 0 1 -1v-2h2a1 1 0 0 0 .993 -.883l.007 -.117a1 1 0 0 0 -1 -1h-2v-2a1 1 0 0 0 -.883 -.993zm1 -8c1.094 0 1.828 .533 2.374 1.514a1 1 0 1 1 -1.748 .972c-.221 -.398 -.342 -.486 -.626 -.486h-10c-.548 0 -1 .452 -1 1v9.998c0 .32 .154 .618 .407 .805l.1 .065a1 1 0 1 1 -.99 1.738a3 3 0 0 1 -1.517 -2.606v-10c0 -1.652 1.348 -3 3 -3z" />
            </svg>
            Agregar
          </button>
        </div>
      </div>
    </div>

    <!-- Filtros -->
    <div class="row container-list align-items-center justify-content-center">
      <div class="btn-dropdown col col-md-3" :class="{ active: selected === 'Todas' }">
        <button @click="filterUpdates('Todas')">Todas</button>
      </div>
      <div class="btn-dropdown col  col-md-3" :class="{ active: selected === 'Pendientes' }">
        <button @click="filterUpdates('Pendientes')">Pendientes</button>
      </div>
      <div class="btn-dropdown col  col-md-3" :class="{ active: selected === 'Completadas' }">
        <button @click="filterUpdates('Completadas')">Completadas</button>
      </div>
    </div>

    <!-- Lista de tareas -->
    <div class="container-tasks col-lg p-5 border p-2 mb-2 border-opacity-50 rounded-4">
      <div class="card p-2 d-flex justify-content-center flex-column align-items-center" v-if="filteredTasks.length === 0">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
          stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-calendar-plus">
          <path stroke="none" d="M0 0h24v24H0z" fill="none"/>
          <path d="M12.5 21h-6.5a2 2 0 0 1 -2 -2v-12a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v5" />
          <path d="M16 3v4" />
          <path d="M8 3v4" />
          <path d="M4 11h16" />
          <path d="M16 19h6" />
          <path d="M19 16v6" />
        </svg>
        <h6>No hay ninguna tarea</h6>
        <p>!Agregar una tarea para iniciar!</p>
      </div>

      <ul class="list-group" v-for="(taskList, i) in filteredTasks" v-bind:key="i">
        <li class="list-group-item d-flex justify-content-between">
          <!-- Cambiar estado de la tarea -->
          <span v-on:click="updateTasks(taskList, i)" :class="[taskList.status ? 'bg-sucess' : '', 'cursor']">
            <i style="color: #5400ff" :class="taskList.status ? 'fa fa-square-check' : 'fas fa-square'"></i>
          </span>
          <!-- Nombre de la tarea -->
          <h6>{{ taskList.name }}</h6>
          <!-- Eliminar tarea -->
          <span v-on:click="deleteTasks(i)">
            <i class="fas fa-trash-alt" style="color: #5b22b3"></i>
          </span>
        </li>
      </ul>
    </div>

    
  </div>
  <footer>
      <p class="text-copy text-center mt-5">&copy; 2025 TaskHub. Hazel Chavez Alvarado.</p>
    </footer>
</template>

<script>
export default {
  data() {
    return {
      tasks: [], // Array donde se irán almacenando las tareas
      nameTasks: "", // Nombre de la tarea nueva
      selected: "Todas", // Filtro seleccionado inicialmente
    };
  },
  computed: {
    filteredTasks() {
      // Filtra las tareas según el estado seleccionado
      if (this.selected === "Todas") {
        return this.tasks; // Mostrar todas
      } else if (this.selected === "Completadas") {
        return this.tasks.filter((task) => task.status === true);
      } else if (this.selected === "Pendientes") {
        return this.tasks.filter((task) => task.status === false);
      }
      return this.tasks;
    },
  },
  methods: {
    addTasks() {
      // Crear y agregar tarea
      const taskList = { name: this.nameTasks, status: false };
      this.tasks.push(taskList);
      this.nameTasks = ""; // Limpiar input
      console.log(this.tasks);
    },
    deleteTasks(i) {
      // Eliminar tarea por índice
      this.tasks.splice(i, 1);
    },
    updateTasks(taskList, i) {
      // Cambiar estado de la tarea
      this.tasks[i].status = !taskList.status;
    },
    filterUpdates(status) {
      // Cambiar filtro seleccionado
      this.selected = status;
    },
  },
};
</script>

<style scoped>
/* Encabezado */
.container-header h1 {
  font-family: Segoe UI Emoji;
  text-align: center;
  color: var(--bg-color-logo);
  font-weight: 700;
}
.container-header p {
  text-align: center;
  color: #9275f6;
  font-weight: 600;
  font-size: clamp(14px, 1vw, 18px);
}

/* Estadísticas de tareas */
.container-item {
  width: 25%;
  background: var(--card-bg);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 25px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1rem;
  text-align: center;
}

/* Input para agregar tareas */
.container-input {
  background: var(--card-bg);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 25px;
  border: 1px solid rgba(255, 255, 255, 0.2);
}
input.form-control {
  background-color: var(--card-bg);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: var(--text-color);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  transition: all 0.3s;
}
input.form-control:focus {
  outline: none;
  box-shadow: 0 0 10px var(--bg-color-logo);
  border: 1px solid var(--bg-color-logo);
}
::placeholder {
  font-family: "Ubuntu", sans-serif;
  color: rgb(233, 213, 255);
  opacity: 0.5;
}

/* Botones */
button.btn{
  background: var(--btn-add);
  font-family: "Funnel Sans", sans-serif;
  color: #f5f7f8;
  padding: 0.8rem;
  border-radius: 15px;
  box-shadow: 0 10px 15px -3px rgb(168 85 247 / 0.5),
    0 4px 6px -4px rgb(168 85 247 / 0.5);
  transition: all 0.3s;
}
button.btn:hover {
  background: linear-gradient(135deg, #9333ea 0%, #6b21a8 100%);
  transform: translateY(-2px);
  box-shadow: 0 20px 25px -5px rgb(147 51 234 / 0.6),
              0 10px 10px -5px rgb(147 51 234 / 0.4);
}
button.btn svg {
  margin-right: 0.5rem;
}
.btn:hover {
  opacity: 0.9;
}

/* Lista de tareas */
.container-tasks {
  background-color: var(--card-bg);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 25px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  margin-top: 1rem;
}
.card.p-2 {
  background-color: var(--card-bg);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 15px;
  height: 150px;
}
.card svg {
  color: var(--text-color);
}
.card h6 {
  color: var(--text-color);
  font-weight: 600;
  font-size: clamp(14px, 2.5vw, 18px);
}
.card p {
  color: rgb(233, 213, 255);
  font-size: clamp(12px, 2vw, 18px);
  opacity: 0.5;
}
span i {
  cursor: pointer;
}

/* Dropdown de filtros */
.container-list {
  margin-top: 4rem;
}
.btn-dropdown {
  background: var(--card-bg);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 25px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1rem;
  text-align: center;
  margin-right: 1rem;
  margin-bottom: 1rem;
  cursor: pointer;
  transition: background-color 0.3s;
}
.btn-dropdown button {
  background: none;
  border: none;
  color: var(--text-color);
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
}
.btn-dropdown.active {
  background: var(--bg-color-logo);
  border: 1px solid rgba(255, 255, 255, 0.4);
}
.btn-dropdown.active button {
  color: var(--text-color-secondary);
}

/* Footer */
.text-copy {
  color: rgb(233, 213, 255);
  font-size: 16px;
  font-weight: 500;
}
</style>

