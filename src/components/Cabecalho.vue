<script setup>
const props = defineProps({ tarefasPendentes: Number });
</script>

<template>
  <header class="p-5 mb-4 mt-4 bg-dark text-white rounded">
    <h1 class="gradient-text">Minhas Tarefas</h1>
    <p>
      Você possui {{ tarefasPendentes }} tarefas pendentes.
    </p>
  </header>
</template>
