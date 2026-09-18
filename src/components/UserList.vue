<template>
  <div class="lista-usuarios">
    <h2>Lista de Usuarios</h2>
    <p v-if="usuarios.length === 0">No hay usuarios registrados.</p>
    
    <ul>
      <li v-for="usuario in usuarios" :key="usuario.id" class="usuario-item">
        <div class="info">
          <strong>{{ usuario.nombre }}</strong> - {{ usuario.email }}
        </div>
        <div class="acciones">
          <button @click="$emit('editar', usuario)" class="btn-editar">Editar</button>
          <button @click="$emit('eliminar', usuario.id)" class="btn-eliminar">Eliminar</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
defineProps(['usuarios']);
defineEmits(['editar', 'eliminar']);
</script>

