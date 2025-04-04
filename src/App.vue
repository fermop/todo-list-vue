<script setup>
  import { ref, reactive, watch, onMounted } from 'vue';
  import { uid } from 'uid'
  import Header from './components/Header.vue';
  import Input from './components/Input.vue';
  import Task from './components/Task.vue';

  const states = reactive({
    nightMode: false
  })

  const toggleNightMode = () => {
    states.nightMode = !states.nightMode
    document.body.classList.toggle('dark');
    localStorage.setItem('dark-mode', states.nightMode)
  }

  const tasks = ref([]);
  const task = reactive({
    id: null,
    description: '',
    checked: null
  })

  watch(tasks, () => {
   guardarLocalStorage()
  }, {
    deep: true
  })

  onMounted(() => {
    const tasksStorage = localStorage.getItem('tasks')

    if (tasksStorage) {
      tasks.value = JSON.parse(tasksStorage)
    }

    const isActive = localStorage.getItem('dark-mode') === 'true'

    if (isActive) {
      toggleNightMode()
    }
  })
  
  const guardarLocalStorage = () => {
    localStorage.setItem('tasks', JSON.stringify(tasks.value))
  }
  
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
    <Header
      @toggle-night-mode="toggleNightMode"
    />

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