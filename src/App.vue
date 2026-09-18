<template>
  <div class="crud-container">
    <h1>Gestión de Usuarios</h1>
    
    <UserForm 
      :usuarioAEditar="usuarioEditando" 
      @guardar="guardarUsuario" 
      @cancelar="cancelarEdicion"
    />

    <UserList 
      :usuarios="usuarios" 
      @editar="prepararEdicion" 
      @eliminar="eliminarUsuario"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import UserForm from './components/UserForm.vue';
import UserList from './components/UserList.vue';

const usuarios = ref([
  { id: 1, nombre: 'Ana Garcia', email: 'ana@example.com' },
  { id: 2, nombre: 'Carlos Lopez', email: 'carlos@example.com' }
]);

const usuarioEditando = ref(null);

const guardarUsuario = (usuario) => {
  if (usuario.id) {
    const index = usuarios.value.findIndex(u => u.id === usuario.id);
    if (index !== -1) usuarios.value[index] = usuario;
  } else {
    usuarios.value.push({
      id: Date.now(),
      nombre: usuario.nombre,
      email: usuario.email
    });
  }
  usuarioEditando.value = null; //reinicia el estado de edicion
};

const prepararEdicion = (usuario) => {
  usuarioEditando.value = usuario;
};

const eliminarUsuario = (id) => {
  usuarios.value = usuarios.value.filter(u => u.id !== id);
};

const cancelarEdicion = () => {
  usuarioEditando.value = null;
};
</script>

