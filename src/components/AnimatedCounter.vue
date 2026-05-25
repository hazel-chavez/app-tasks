<template>
	<span ref="counter">{{ displayNumber }}</span>
</template>
<script>
import { ref, watch, onMounted } from 'vue';
import { CountUp } from 'countup.js';

/**
 * Componente para animar un número usando CountUp.js.
 */

export default {
	props: {
		number: {
			type: Number,
			required: true,
		},
		duration: {
			type: Number,
			default: 1.5,
		},
	},
	/**
	 * @param {{ number: number, duration: number }} props
	 * @returns {{ counter: import('vue').Ref<HTMLElement | null>, displayNumber: import('vue').Ref<number> }}
	 */
	setup(props) {
		const counter = ref(null);
		const displayNumber = ref(0);
		let countUpInstance = null;

		/**
		 * Inicia la animación en el primer render y actualiza el valor en cambios posteriores.
		 * @returns {void}
		 */
		const animate = () => {
			if (countUpInstance) {
				countUpInstance.update(props.number);
			} else {
				countUpInstance = new CountUp(counter.value, props.number, {
					duration: props.duration,
				});
				countUpInstance.start();
			}
		};

		watch(
			() => props.number,
			() => {
				animate();
			},
		);

		onMounted(() => {
			animate();
		});

		return { counter, displayNumber };
	},
};
</script>
