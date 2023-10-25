<script setup>
  import { reactive } from 'vue';
  import Header from './components/Header.vue'
  import Form from './components/Form.vue'
  import TaskList from './components/TaskList.vue'
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
    <Header :tarefas-pendentes="getTarefaPendentes().length"></Header>
    <Form :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefaTemporaria ="estado.tarefatemp" :edtaTarefaTemp="evento => estado.tarefaTemporaria = evento.target.value" :cadastraTarefa="cadastraTarefa"></Form>
    <TaskList :tarefas="getTarefaFiltradas()"></TaskList>
    
    
  </div>
</template>
<style scoped>

.done{
  text-decoration: line-through;
}
</style>


