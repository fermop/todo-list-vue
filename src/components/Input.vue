<script setup>
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
			return
		}

		emit('add-task')
  }
</script>

<template>
  <div class="bg-slate-900 w-full m-auto mb-10 p-5 rounded border-1 border-gray-700">
    <h2 class="text-xl text-white font-bold text-center mb-5">Add task</h2>

    <form
      class="flex gap-5"
      @submit.prevent="validar"
    >

      <input 
        type="text" 
        placeholder="e.g. Buy groceries"
        class="bg-gray-300 p-2 pl-5 w-full rounded border-1 border-gray-700"
        @input="$emit('update:description', $event.target.value)"
        :value="description"
      >
      <button 
      class="bg-lime-950 text-white font-bold w-[4rem] rounded border-1 border-gray-700 cursor-pointer hover:opacity-[.7] duration-250 text-2xl"
      >+</button>
    </form>
  </div>
</template>