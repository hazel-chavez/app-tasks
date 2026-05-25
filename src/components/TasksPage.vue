<template>
	<div class="container p-5">
		<header>
			<div class="container-header">
				<span class="navbar-brand mb-0 h1">
					<h1>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="32"
							height="32"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
							class="icon icon-tabler icons-tabler-outline icon-tabler-list-details"
						>
							<path
								stroke="none"
								d="M0 0h24v24H0z"
								fill="none"
							/>
							<path d="M13 5h8" />
							<path d="M13 9h5" />
							<path d="M13 15h8" />
							<path d="M13 19h5" />
							<path
								d="M3 4m0 1a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v4a1 1 0 0 1 -1 1h-4a1 1 0 0 1 -1 -1z"
							/>
							<path
								d="M3 14m0 1a1 1 0 0 1 1 -1h4a1 1 0 0 1 1 1v4a1 1 0 0 1 -1 1h-4a1 1 0 0 1 -1 -1z"
							/></svg
						>TaskHub
					</h1>
				</span>
				<p class="subtitle">Gestiona tus Tareas de forma Rapida</p>
				<div class="row justify-content-center mb-5 align-items-center">
					<div class="col-12">
						<div
							class="d-flex flex-wrap justify-content-around stats-bar rounded-4"
						>
							<div
								v-for="(count, category) in taskCounts"
								:key="category"
								class="text-center container-item rounded-4"
							>
								<p class="mb-0 text-white-50">{{ category }}</p>
								<h3 class="text-white">
									<AnimatedCounter :number="count" />
								</h3>
							</div>
						</div>
					</div>
				</div>
			</div>
		</header>

		<div class="container">
			<div class="row justify-content-center container-input mb-4 p-5">
				<div
					class="col-12 col-md-8 d-flex justify-content-center align-items-center"
				>
					<input
						type="text"
						class="form-control task-input me-2"
						placeholder="Agregar nueva tarea..."
						v-model="nameTasks"
						@keyup.enter="addTasks()"
					/>
					<button
						type="button"
						class="btn d-flex align-items-center"
						v-on:click="addTasks()"
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							width="24"
							height="24"
							viewBox="0 0 24 24"
							fill="currentColor"
							class="icon icon-tabler icons-tabler-filled icon-tabler-copy-plus"
						>
							<path
								stroke="none"
								d="M0 0h24v24H0z"
								fill="none"
							/>
							<path
								d="M18.333 6a3.667 3.667 0 0 1 3.667 3.667v8.666a3.667 3.667 0 0 1 -3.667 3.667h-8.666a3.667 3.667 0 0 1 -3.667 -3.667v-8.666a3.667 3.667 0 0 1 3.667 -3.667zm-4.333 4a1 1 0 0 0 -1 1v2h-2a1 1 0 0 0 -.993 .883l-.007 .117a1 1 0 0 0 1 1h2v2a1 1 0 0 0 .883 .993l.117 .007a1 1 0 0 0 1 -1v-2h2a1 1 0 0 0 .993 -.883l.007 -.117a1 1 0 0 0 -1 -1h-2v-2a1 1 0 0 0 -.883 -.993zm1 -8c1.094 0 1.828 .533 2.374 1.514a1 1 0 1 1 -1.748 .972c-.221 -.398 -.342 -.486 -.626 -.486h-10c-.548 0 -1 .452 -1 1v9.998c0 .32 .154 .618 .407 .805l.1 .065a1 1 0 1 1 -.99 1.738a3 3 0 0 1 -1.517 -2.606v-10c0 -1.652 1.348 -3 3 -3z"
							/>
						</svg>
						Agregar
					</button>
				</div>
			</div>
		</div>

		<div class="row container-list align-items-center justify-content-center">
			<div
				class="btn-dropdown col col-md-3"
				:class="{ active: selected === 'Todas' }"
			>
				<button @click="filterUpdates('Todas')">Todas</button>
			</div>
			<div
				class="btn-dropdown col col-md-3"
				:class="{ active: selected === 'Pendientes' }"
			>
				<button @click="filterUpdates('Pendientes')">Pendientes</button>
			</div>
			<div
				class="btn-dropdown col col-md-3"
				:class="{ active: selected === 'Completadas' }"
			>
				<button @click="filterUpdates('Completadas')">Completadas</button>
			</div>
		</div>

		<div
			class="container-tasks col-lg p-5 border p-2 mb-2 border-opacity-50 rounded-4"
		>
			<div
				class="card p-2 mt-3 d-flex justify-content-center flex-column align-items-center"
				v-if="filteredTasks.length === 0"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="24"
					height="24"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
					class="icon icon-tabler icons-tabler-outline icon-tabler-calendar-plus"
				>
					<path
						stroke="none"
						d="M0 0h24v24H0z"
						fill="none"
					/>
					<path
						d="M12.5 21h-6.5a2 2 0 0 1 -2 -2v-12a2 2 0 0 1 2 -2h12a2 2 0 0 1 2 2v5"
					/>
					<path d="M16 3v4" />
					<path d="M8 3v4" />
					<path d="M4 11h16" />
					<path d="M16 19h6" />
					<path d="M19 16v6" />
				</svg>
				<h6>No hay ninguna tarea</h6>
				<p>!Agregar una tarea para iniciar!</p>
			</div>

			<ul
				class="list-group"
				v-for="(taskList, i) in filteredTasks"
				v-bind:key="i"
			>
				<li class="list-group-item d-flex justify-content-between">
					<span
						v-on:click="updateTasks(taskList, i)"
						:class="[taskList.status ? 'bg-sucess' : '', 'cursor']"
					>
						<i
							style="color: #5400ff"
							:class="taskList.status ? 'fa fa-square-check' : 'fas fa-square'"
						></i>
					</span>
					<h6>{{ taskList.name }}</h6>
					<span v-on:click="deleteTasks(i)">
						<i
							class="fas fa-trash-alt"
							style="color: #5b22b3"
						></i>
					</span>
				</li>
			</ul>
		</div>
	</div>
	<footer>
		<p class="text-copy text-center mt-5">
			&copy; 2026 TaskHub. Hazel Chavez Alvarado.
		</p>
	</footer>
</template>

<script>
import AnimatedCounter from './AnimatedCounter.vue';

/**
 * @typedef {Object} Task
 * @property {string} name Nombre de la tarea.
 * @property {boolean} status Estado de la tarea; true si está completada.
 */

export default {
	components: {
		AnimatedCounter,
	},
	/**
	 * Estado local del módulo de tareas.
	 * @returns {{ tasks: Task[], nameTasks: string, selected: 'Todas' | 'Pendientes' | 'Completadas' }}
	 */
	data() {
		return {
			/** @type {Task[]} */
			tasks: [],
			nameTasks: '',
			selected: 'Todas',
		};
	},
	computed: {
		/**
		 * Resumen de tareas por categoría para la barra de estadísticas.
		 * @returns {{ Todas: number, Pendientes: number, Completadas: number }}
		 */
		taskCounts() {
			const counts = {};
			counts.Todas = this.tasks.length;
			counts.Pendientes = this.tasks.filter((task) => !task.status).length;
			counts.Completadas = this.tasks.filter((task) => task.status).length;
			return counts;
		},
		/**
		 * Devuelve la lista de tareas según el filtro seleccionado.
		 * @returns {Task[]}
		 */
		filteredTasks() {
			if (this.selected === 'Todas') {
				return this.tasks;
			} else if (this.selected === 'Completadas') {
				return this.tasks.filter((task) => task.status === true);
			} else if (this.selected === 'Pendientes') {
				return this.tasks.filter((task) => task.status === false);
			}
			return this.tasks;
		},
	},
	methods: {
		/**
		 * Agrega una nueva tarea en estado pendiente.
		 * Si el campo está vacío, no agrega nada.
		 * @returns {void}
		 */
		addTasks() {
			const taskList = { name: this.nameTasks, status: false };
			this.tasks.push(taskList);
			this.nameTasks = '';
		},
		/**
		 * Elimina una tarea por índice.
		 * @param {number} i Índice de la tarea.
		 * @returns {void}
		 */
		deleteTasks(i) {
			this.tasks.splice(i, 1);
		},
		/**
		 * Cambia el estado de una tarea (pendiente/completada).
		 * @param {Task} taskList Tarea actual.
		 * @param {number} i Índice de la tarea en la lista.
		 * @returns {void}
		 */
		updateTasks(taskList, i) {
			this.tasks[i].status = !taskList.status;
		},
		/**
		 * Actualiza el filtro activo para la vista de tareas.
		 * @param {'Todas' | 'Pendientes' | 'Completadas'} status Estado de filtro seleccionado.
		 * @returns {void}
		 */
		filterUpdates(status) {
			this.selected = status;
		},
	},
};
</script>

<style scoped>
.container-header h1 {
	font-family: var(--font-logo);
	text-align: center;
	color: var(--bg-color-logo);
	font-weight: bold;
	font-size: 3rem;
}

.container-header .subtitle {
	font-size: clamp(18px, 1vw, 18px);
	font-family: var(--font-general);
}

.container-header p {
	text-align: center;
	color: #9275f6;
	font-weight: 600;
	font-size: clamp(14px, 1vw, 18px);
	font-family: var(--font-general);
}

.container-item h3 {
	font-size: clamp(24px, 4vw, 32px);
	font-weight: bold;
	font-family: var(--font-general);
}

.container-item {
	width: 25%;
	background: var(--card-bg);
	backdrop-filter: blur(15px);
	-webkit-backdrop-filter: blur(15px);
	border-radius: 25px;
	border: 1px solid rgba(255, 255, 255, 0.2);
	padding: 1rem;
	text-align: center;
	font-family: var(--font-general);
}

.container-input {
	background: var(--card-bg);
	backdrop-filter: blur(15px);
	-webkit-backdrop-filter: blur(15px);
	border-radius: 25px;
	border: 1px solid rgba(255, 255, 255, 0.2);
	font-family: var(--font-general);
}

input.form-control {
	background-color: var(--card-bg);
	border: 1px solid rgba(255, 255, 255, 0.2);
	color: var(--text-color);
	backdrop-filter: blur(15px);
	-webkit-backdrop-filter: blur(15px);
	transition: all 0.3s;
	font-family: var(--font-general);
}

input.form-control:focus {
	outline: none;
	box-shadow: 0 0 10px var(--bg-color-logo);
	border: 1px solid var(--bg-color-logo);
}

::placeholder {
	font-family: 'Ubuntu', sans-serif;
	color: rgb(233, 213, 255);
	opacity: 0.5;
	font-size: clamp(14px, 2vw, 18px);
}

button.btn {
	background: var(--btn-add);
	font-family: 'Funnel Sans', sans-serif;
	color: #f5f7f8;
	padding: 0.8rem;
	border-radius: 15px;
	box-shadow: 0 10px 15px -3px rgb(168 85 247 / 0.5),
		0 4px 6px -4px rgb(168 85 247 / 0.5);
	transition: all 0.3s;
	font-family: var(--font-general);
}

button.btn:hover {
	background: var(--btn-add-hover);
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

.container-tasks {
	min-height: 300px;
	background-color: var(--card-bg);
	backdrop-filter: blur(15px);
	-webkit-backdrop-filter: blur(15px);
	border-radius: 25px;
	border: 1px solid rgba(255, 255, 255, 0.2);
	margin-top: 1rem;
	font-family: var(--font-general);
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

.container-list {
	margin-top: 4rem;
	font-family: var(--font-general);
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

ul.list-group li.list-group-item {
	background: var(--card-bg);
	backdrop-filter: blur(15px);
	-webkit-backdrop-filter: blur(15px);
	border: none;
	border-bottom: 1px solid rgba(255, 255, 255, 0.2);
	color: var(--text-color);
	font-weight: 600;
	font-size: clamp(14px, 2.5vw, 18px);
}

.text-copy {
	color: rgb(233, 213, 255);
	font-size: 16px;
	font-weight: 500;
	font-family: var(--font-general);
}
</style>
