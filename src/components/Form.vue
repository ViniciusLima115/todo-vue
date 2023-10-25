
<script setup>
    const props = defineProps(["cadastraTarefa","tarefaTemp","trocarFiltro","editaTarefaTemp"])
        
    
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required type="text" placeholder="Digite Aqui a descricao da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="props.trocarFiltro" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadass</option>
          </select>
        </div>
      </div>
    </form>
</template>