<script setup>

const props = defineProps(['tarefas'])
const todasConcluidas = () =>{
    return props.tarefas.every(tarefa => tarefa.concluida);
}

</script>
<template>
<p v-if="todasConcluidas()" class="alert alert-success">
    Parabéns! Você concluiu todas as tarefas!
</p>

<ul class="list-group mt-4">
    <li class="list-group-item" v-for= "tarefa in props.tarefas">
    <input @change="evento => tarefa.concluida = evento.target.checked" :checked="tarefa.concluida" :id="tarefa.titulo" type="checkbox">
    <label :class="{done: tarefa.concluida === true}" class="ms-3" :for="tarefa.titulo">
    {{ tarefa.titulo }}
    </label>
    </li>
</ul>

</template>

<style scoped>

.done {
    text-decoration: line-through;
}

</style>