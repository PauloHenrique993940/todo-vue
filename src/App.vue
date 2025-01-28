<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefa from './components/ListaDeTarefa.vue';

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
    },
  ],
});

// Função para cadastrar uma nova tarefa
const cadastrarTarefa = () => {
  if (estado.tarefaTemp.trim() === '') return; // Evita adicionar tarefas vazias
  estado.tarefas.push({
    titulo: estado.tarefaTemp,
    finalizada: false,
  });
  estado.tarefaTemp = ''; // Limpa o campo de entrada após o cadastro
};

// Função para obter tarefas filtradas
const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes':
      return estado.tarefas.filter((tarefa) => !tarefa.finalizada);
    case 'finalizadas':
      return estado.tarefas.filter((tarefa) => tarefa.finalizada);
    default:
      return estado.tarefas;
  }
};
</script>

<template>
  <div class="container bg-custom">
    <Cabecalho :tarefas-pendentes="estado.tarefas.filter(tarefa => !tarefa.finalizada).length" />

    <Formulario
      :tarefa-temp="estado.tarefaTemp"
      @update:tarefaTemp="estado.tarefaTemp = $event"
      @cadastrar-tarefa="cadastrarTarefa"
    />

    <ListaDeTarefa :tarefas="getTarefasFiltradas()" />
  </div>
</template>



