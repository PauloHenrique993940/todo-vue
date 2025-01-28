<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar Sass',
      finalizada: false,
    },
    {
      titulo: 'Ir à academia',
      finalizada: false,
    }
  ]
});

// Função que filtra as tarefas pendentes
const getNumeroTarefaPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada);
};

// Função que filtra as tarefas finalizadas
const getNumeroTarefaFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada);

};

// Função que retorna as tarefas filtradas conforme o estado do filtro
const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes':
      return getNumeroTarefaPendentes();
    case 'finalizadas':
      return getNumeroTarefaFinalizadas();
    default:
      return estado.tarefas; // Retorna todas as tarefas
  }
};

const cadastrarTarefa = (e) => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';

}
</script>

<template>
  <div class="container bg bg-custom">
    <header class="p-5 mb-4 mt-4 bg-dark text-white rounded header">       
      <h1 class="gradient-text">{Minhas tarefas}</h1>
      <p>Você possui {{ getNumeroTarefaPendentes().length }} tarefas pendentes.</p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required
            type="text"
            placeholder="Digite aqui a descrição da tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()" :key="tarefa.titulo">
        <input @change="evento => tarefa.finalizada = evento.target.checked"
          v-model="tarefa.finalizada"
          :id="tarefa.titulo"
          type="checkbox"
        />
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
  color: rgba(7, 33, 105, 0.801);
  font-family: Roboto, sans-serif;
}
</style>

