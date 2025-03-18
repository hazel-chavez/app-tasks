
<template>
  <div class="container p-5">
  <header>
    <div class="container-header">
      <nav class="navbar row">
        <div class="container">
          <span class="navbar-brand mb-0 h1">
            <img
              alt="logo"
              class="logo"
              src="@/assets/Logo-app.png"
             width="105" height="100"
            />
          </span>
        </div>
        <div class="row d-flex justify-content-center container-input">
          <div class="col-lg-6 offset-1g-2 mb-2">
            <input
              type="text"
              class="form-control form-control-lg"
              placeholder="Ingresar Tarea"
               v-model="nameTasks"

            />
          <div class="container-button col d-flex justify-content-center pt-3">
            <button type="button" class="btn btn-outline  justify-content-center text-center"
            v-on:click="addTasks()">Agregar Tarea<img src="@/assets/boton-agregar.png"></button>
            <!-- metodo agregue las tareas -->
          </div>

          </div>
        </div>
      </nav>
    </div>
  </header>

  <div class="container row pt-5 ">


    <div class="col-lg offset offset-lg container-tasks p-5 border  p-2 mb-2 border-opacity-50 rounded-4">
      <!-- condicion para que quite las tareas -->
    <div class="dropdown mb-3">
  <button class="btn btn-secondary dropdown-toggle"    type="button" data-bs-toggle="dropdown" aria-expanded="false">
  Filtrar Tareas ({{ selected }})
  <!-- aparecera lo que seleccione el usuario -->
  </button>
  <ul class="dropdown-menu">
    <li><a class="dropdown-item" href="#" @click.prevent="filterUpdates('Todas')">Todas</a></li>
    <li><a class="dropdown-item" href="#" @click.prevent="filterUpdates('Pendientes')">Pendientes</a></li>
    <li><a class="dropdown-item" href="#" @click.prevent="filterUpdates('Completadas')">Completadas</a></li>
  </ul>
</div>
      <div class="card p-2" v-if="filteredTasks.length === 0">
        <h6>No hay ninguna tarea</h6>
      </div>
      <ul class="list-group" v-for="(taskList, i) in filteredTasks" v-bind:key="i">
        <!-- imprimimos las cards con las tareas  -->
        <li class="list-group-item d-flex justify-content-between">
          <span
            v-on:click="updateTasks(taskList, i)"
            v-bind:class="[
              taskList.status === true ? 'bg-sucess' : '',
              'cursor',
            ]"
          >
            <i
              style="color: #3887BE"
              v-bind:class="[
                taskList.status === true
                  ? 'fa fa-square-check'
                  : 'fas fa-square',
              ]"
            ></i>
            <!-- array para que cambie el estado de actualizacion de la tarea -->
          </span>
          <!-- agregar el nombre de la tareas -->
          <h6>   {{ taskList.name }}</h6>
          <!-- llamamos al metodo y le pasamos como parametro el valor de i para saber que tarea eliminar -->
          <span v-on:click="deleteTasks(i)">
            <i class="fas fa-trash-alt" style="color: #3887BE"></i>
          </span>
        </li>
      </ul>
    </div>
  </div>
</div>
</template>
<script>
export default {
  data() {
    return {
      tasks: [], //array donde se iran almacenando las tareas
      nameTasks: "",
      selected: 'Todas', // option sera seleccionado como valor inicial
    }
  },
  // establecer comparaciones y lógica elaborada que se reevalúa cada vez que uno de sus valores a comprobar cambia, asegurando su reactividad
  computed: {
    filteredTasks() {
      if (this.selected === 'Todas') {//segun lo que seleccion el usuario se filtre con su estado
       // Mostrar todas las tareas
        return this.tasks;
      } else if (this.selected === 'Completadas') {
          // Mostrar solo tareas completadas
        return this.tasks.filter(task => task.status === true);//completadas
      } else if (this.selected === 'Pendientes') {
        // Mostrar solo tareas pendientes
        return this.tasks.filter(task => task.status === false);//pendientes
      }
      return this.tasks;
    },
  },
  methods: {
    addTasks() {
      // Crear el objeto de la tarea
      const taskList = {
        name: this.nameTasks, // Nombre de la tarea
        status: false, // Estado inicial de la tarea (incompleta)
      };

      // Agregar el objeto taskList al array tasks
      this.tasks.push(taskList);

      // Limpiar las tareas
      this.nameTasks = "";

      console.log(this.tasks);
    },
    deleteTasks(i) {
      this.tasks.splice(i, 1); //i es la posicion del elemento y se eliminara solo 1
    },
    updateTasks(taskList, i) {
      this.tasks[i].status = !taskList.status;//invertir el estado de la tarea
    },
    //Cambiar el filtro seleccionado.
    filterUpdates(status){
      this.selected = status;

    }
  },
};
</script>
<style scoped>
.container.p-5{
background-color:#f3faf8;
-webkit-box-shadow: 4px 9px 81px -1px rgba(0,0,0,0.75);
-moz-box-shadow: 4px 9px 81px -1px rgba(0,0,0,0.75);
box-shadow: 4px 9px 81px -1px rgba(0,0,0,0.75);
}

.navbar {
  display: flex;
  background-image: url(@/assets/imgHeader.jpg);
  border-radius: 15px;

}
input.form-control.form-control-lg{
  background-color: var(--bg-btn);
}
::placeholder {
  color: rgb(180, 178, 178);
  font-family: "Ubuntu", sans-serif;
}
.container-card{
  background-color: var(--bg-card);
  height: 35vw;
}
div.card{
  background-color: var(--bg-btn);
}
li.list-group-item.d-flex.justify-content-between {
  background-color: var(--bg-cardTasks);
}
.btn {
  background-color:#24c5b0;
  font-family: "Funnel Sans", sans-serif;
  color: #F5F7F8;
}
.btn:hover{
  color:#87CEEB;
}
.container-tasks{
  background-color: var(--bg-card);

  height: 50vw;

}
h6 {
  color: var(--color-placeholder);

}
span i {
  cursor: pointer;
}
</style>
