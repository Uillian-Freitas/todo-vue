<script setup>

const props = defineProps(['cadastrarTarefa', 'tarefaTemp', 'trocarFiltro', 'editarTarefaTemp']);


</script>

<template>

<form @submit.prevent="props.cadastrarTarefa">
    <div class="row">
    <div class="col">
    <input :value="props.tarefaTemp" @change="props.editarTarefaTemp" required type="text" placeholder="Digite aqui a discrição da tarefa" class="form-control">
    </div>
    <div class="col-md-1">
    <button type="submit" class="btn btn-primary">cadastrar</button>
    </div>
    <div class="col-md-2">
    <select @change="props.trocarFiltro" class="form-control">
    <option value="todas"> Todas as tarefas</option>
    <option value="pendentes"> Todas as pendentes</option>
    <option value="finalizadas"> Todas as finalizadas</option>
    </select>
    </div>
    </div>
</form>

</template>