<template>
  <form @submit.prevent="submit" class="formulario">
    <input v-model="formulario.nombre" type="text" placeholder="Nombre" required />
    <input v-model="formulario.email" type="email" placeholder="Email" required />
    
    <button type="submit">
      {{ usuarioAEditar ? 'Actualizar' : 'Añadir' }}
    </button>
    <button type="button" v-if="usuarioAEditar" @click="cancelar" class="btn-cancelar">
      Cancelar
    </button>
  </form>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['usuarioAEditar']);
const emit = defineEmits(['guardar', 'cancelar']);

const formulario = ref({ id: null, nombre: '', email: '' });

// Observar si el padre envía un usuario para editar y llenar el formulario
watch(() => props.usuarioAEditar, (nuevoValor) => {
  if (nuevoValor) {
    formulario.value = { ...nuevoValor };
  } else {
    formulario.value = { id: null, nombre: '', email: '' };
  }
});

const submit = () => {
  emit('guardar', { ...formulario.value });
  if (!props.usuarioAEditar) {
    formulario.value = { id: null, nombre: '', email: '' }; //limpia si es nuevo
  }
};

const cancelar = () => {
  emit('cancelar');
};
</script>

