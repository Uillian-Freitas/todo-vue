<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefa: [
    {
      titulo: 'Estudar Vue.js',
      concluida: false
    },
    {
      titulo: 'estudar javascript',
      concluida: false
    },
    {
      titulo: 'ir para academia',
      concluida: true
    }
  ]
});

const getTarefasPendentes = () =>{
  return estado.tarefa.filter(tarefa => !tarefa.concluida);
}

const getTarefasfiltradas = () => {
  const {filtro} = estado;

  switch (filtro) {
    case 'todas':
      return estado.tarefa;
    case 'pendentes':
      return estado.tarefa.filter(tarefa => !tarefa.concluida);
    case 'finalizadas':
      return estado.tarefa.filter(tarefa => tarefa.concluida);
    default:
      return estado.tarefa;
  }
}

const cadastrarTarefa = (evento) => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    concluida: false
  };
  estado.tarefa.push(tarefaNova);
  estado.tarefaTemp = '';
}
</script>

<template>
<div class="container">
  <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
  <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :cadastrar-tarefa="cadastrarTarefa" :editar-tarefa-temp="(evento) => estado.tarefaTemp = evento.target.value"/>
 <ListaDeTarefas :tarefas="getTarefasfiltradas()" />
</div>
</template>


