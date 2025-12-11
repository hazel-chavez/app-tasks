<template>
  <span ref="counter">{{ displayNumber }}</span>
  <!-- /*usamos ref para obtener una referencia directa al elemento HTML donde CountUp va a animar el número.*/ -->
</template>
<script>
import { ref, watch, onMounted } from "vue";
import { CountUp } from "countup.js";
/*ref → permite crear referencias reactivas (variables que Vue puede “vigilar”).
watch → sirve para observar cambios en props o variables y ejecutar código cuando cambian.
onMounted → se ejecuta cuando el componente ya se montó en el DOM.
CountUp → la librería que hace la animación de los números.*/

export default {
  props: {
    number: {
      type: Number,/*el número final que queremos mostrar con animación.*/
      required: true,
    },
    duration: {
      type: Number,
      default: 1.5, // duración de la animación en segundos
    },
  },
  setup(props) {
    const counter = ref(null); /*referencia al elemento HTML donde se mostrará el número animado.*/
    const displayNumber = ref(0);/*número que se muestra inicialmente antes de la animación.*/
    let countUpInstance = null;/*instancia de CountUp que manejará la animación del número.*/

    const animate = () => {/*función que inicia o actualiza la animación del número.*/
      if (countUpInstance) {/*si ya existe una instancia de CountUp, simplemente actualizamos el número final.*/
        countUpInstance.update(props.number);
      } else {/*si no existe, creamos una nueva instancia y la iniciamos.*/
        countUpInstance = new CountUp(counter.value, props.number, {
          duration: props.duration,
        });//crea una nueva instancia de CountUp con el elemento HTML, el número final y la duración.
        countUpInstance.start();
      }
    };
/*observa cambios en la prop number y llama a la función animate para actualizar la animación cuando el número cambie.*/
    watch(() => props.number, () => {
      animate();
    });
/*cuando el componente se monta en el DOM, llamamos a la función animate para iniciar la animación inicial.*/
    onMounted(() => {
      animate();
    });
/*retornamos las referencias y variables necesarias para usarlas en el template.*/
    return { counter, displayNumber };
  },
};
</script>
