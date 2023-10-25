<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemporaria: '',
    tarefas:[{
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar VueJS',
      finalizada:false,
    },
    {
      titulo: 'Estudar JS',
      finalizada:true,
    }
  ]
  })

  const getTarefaPendentes = () =>{
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }
  const getTarefaFinalizadas = () =>{
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefaFiltradas = () =>{
    const {filtro} = estado;

    switch(filtro){
      case 'pendentes':
        return getTarefaPendentes();
      case 'finalizadas':
        return getTarefaFinalizadas();
      default:
        return estado.tarefas  
    }
  }

  const cadastraTarefa = () =>{
    const tarefaNova = {
      titulo: estado.tarefaTemporaria,
      finalizada : false,
    }
    estado.tarefas.push(tarefaNova)
    estado.tarefaTemporaria = "";
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Voce Possui {{getTarefaPendentes().length}} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required type="text" placeholder="Digite Aqui a descricao da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadass</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefaFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>
<style scoped>

.done{
  text-decoration: line-through;
}
</style>


