<script setup>
  import { ref, reactive } from 'vue';
  import { uid } from 'uid'
  import Header from './components/Header.vue';
  import Input from './components/Input.vue';
  import Task from './components/Task.vue';

  const tasks = ref([]);
  const task = reactive({
    id: null,
    description: '',
    checked: null
  })
  
  const addTask = () => {
    tasks.value.unshift({
      ...task,
      id: uid(),
      checked: false
    })
    
    task.description = ''
  }

  const HandleCheckboxChange = (id) => {
    const i = tasks.value.findIndex(taskstate => taskstate.id === id)
    tasks.value[i].checked = !tasks.value[i].checked
  }

  const deleteTask = (id) => {
    tasks.value = tasks.value.filter(task => task.id !== id)
  }
</script>

<template>
  <div class="w-full m-auto p-5 max-w-5xl">
    <Header/>

    <Input
      v-model:description="task.description"
      v-model:checked="task.checked"
      :id="task.id"
      @add-task="addTask"
    />
    
    <div v-if="tasks.length">
      <Task
        v-for="task in tasks"
        :task="task"
        @handle-checkbox-change="HandleCheckboxChange"
        @delete-task="deleteTask"
      />
    </div>
  </div>
</template>