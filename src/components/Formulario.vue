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
        />
      </div>
      <div class="col-md-2">
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

<style scoped>
/* Estilo para telas maiores */
.cadastro input {
  width: 100%;
  height: 40px;
}

.cadastro .button {
  width: 100%;
}

/* Responsividade para telas menores (até 420px) */
@media (max-width: 420px) {
  .cadastro {
    display: flex;
    flex-direction: column;
    gap: 20px;
    text-align: center;
  }

  .cadastro input {
    width: 100%;
  }

  .cadastro .button {
    width: 100%;
  }

  .cadastro select {
    width: 100%;
  }
}
</style>

