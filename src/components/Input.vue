<script setup>
  import { ref } from 'vue'
  import Alert from './Alert.vue'

  const error = ref(false)

  const emit = defineEmits(['update:description', 'update:checked', 'add-task'])

  const props = defineProps({
    id: {
      type: [String, null],
      required: true
    },
    description: {
      type: String,
      required: true
    },
    checked: {
      type: [null, Boolean],
      required: true
    }
  })

  const validar = () => {
		if (Object.values(props).includes('')) {
      error.value = true
      setTimeout(() => {
        error.value = false
      }, 2000);
			return
		}

		emit('add-task')
  }
</script>

<template>
  <Alert
    v-if="error"
  />
  <div class="bg-slate-200 dark:bg-slate-800 w-full m-auto mb-10 p-5 rounded border-1 border-gray-700">
    <h2 class="text-xl text-slate-700 dark:text-white font-bold text-center mb-5">Add task</h2>

    <form
      class="flex gap-5"
      @submit.prevent="validar"
    >

      <input 
        type="text" 
        placeholder="e.g. Buy groceries"
        class="bg-slate-100 dark:bg-gray-300 p-2 pl-5 w-full rounded border-1 border-gray-700"
        @input="$emit('update:description', $event.target.value)"
        :value="description"
      >
      <button 
      class="bg-lime-300 dark:bg-lime-950 text-slate-900 dark:text-white font-bold w-[4rem] rounded border-1 border-gray-700 cursor-pointer hover:opacity-[.7] duration-250 text-2xl"
      >+</button>
    </form>
  </div>
</template>