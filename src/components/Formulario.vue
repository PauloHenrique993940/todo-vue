<script setup>
const props = defineProps(['tarefaTemp']);
const emits = defineEmits(['update:tarefaTemp', 'cadastrar-tarefa']);
</script>

<template>
  <form @submit.prevent="$emit('cadastrar-tarefa')">
    <div class="row text-center cadastro">
      <div class="col-md-8">
        <input
          :value="tarefaTemp"
          @input="$emit('update:tarefaTemp', $event.target.value)"
          required
          type="text"
          placeholder="Digite a descrição da sua tarefa"
          style="width: 100%; height: 40px;"
        />
      </div>
      <div class="col-md-2 ">
        <button type="submit" class="btn btn-primary button">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="$emit('troca-filtro', $event.target.value)" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
