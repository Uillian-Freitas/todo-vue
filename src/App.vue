<script setup>
import { reactive } from 'vue';

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

  <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Minha lista de tarefas</h1>

    <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
  </header>

<form @submit.prevent="cadastrarTarefa">
  <div class="row">
    <div class="col">
      <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite aqui a discrição da tarefa" class="form">
    </div>
    <div class="col-md-1">
      <button type="submit" class="btn btn-primary">cadastrar</button>
    </div>
    <div class="col-md-2">
      <select @change="evento => estado.filtro = evento.target.value" class="form-control">
      <option value="todas"> Todas as tarefas</option>
      <option value="pendentes"> Todas as pendentes</option>
      <option value="finalizadas"> Todas as finalizadas</option>
    </select>
    </div>
  </div>
</form>
<ul class="list-group mt-4">
  <li class="list-group-item" v-for= "tarefa in getTarefasfiltradas()">
    <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" :id="tarefa.titulo" type="checkbox">
    <label :class="{done: tarefa.concluida === true}" class="ms-3" :for="tarefa.titulo">
      {{ tarefa.titulo }}
    </label>
  </li>
</ul>
</div>

</template>

<style scoped>

.done {
  text-decoration: line-through;
}

</style>
