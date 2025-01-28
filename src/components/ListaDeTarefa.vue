<script setup>
const props = defineProps(['tarefas']);
const removeTarefa = (tarefa) => {
  const index = props.tarefas.indexOf(tarefa);
  if (index > -1) {
    props.tarefas.splice(index, 1);
  }
};
</script>

<template>
  <ul class="list-group mt-4">
    <li 
      class="list-group-item d-flex align-items-center justify-content-between" 
      v-for="tarefa in tarefas" 
      :key="tarefa.titulo"
    >
      <div>
        <input 
          type="checkbox" 
          v-model="tarefa.finalizada" 
          :id="tarefa.titulo"
        />
        <label 
          :class="{ done: tarefa.finalizada }" 
          class="ms-3" 
          :for="tarefa.titulo"
        >
          {{ tarefa.titulo }}
        </label>
      </div>
      <!-- Botão para remover a tarefa -->
      <button 
        v-if="tarefa.finalizada" 
        class="btn btn-danger btn-sm" 
        @click="removeTarefa(tarefa)"
      >
        Remover
      </button>
    </li>
  </ul>
</template>

<style scoped>
.done {
  text-decoration: line-through;
  color: rgba(7, 33, 105, 0.801);
}
</style>

