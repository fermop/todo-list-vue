<script setup>
	defineProps({
		task: {
			type: Object,
			required: true
		}
	})

	defineEmits(['handle-checkbox-change', 'delete-task'])
</script>

<template>
  <div 
		:class="[!task.checked ? 'opacity-[1]' : 'opacity-[.6]']"
		class="bg-slate-900 w-full m-auto p-5 rounded border-1 border-gray-700 my-3 flex gap-5 duration-250">

    <p class="w-full font-semibold text-gray-300">{{ task.description }}</p>

    <div 
			class="flex gap-5">

			<input 
				type="checkbox"
				class="w-[1.25rem]"
				@change="$emit('handle-checkbox-change', task.id)"
			>
			<button 
				class="bg-red-950 text-white font-bold w-[2rem] rounded border-1 border-gray-700 cursor-pointer hover:opacity-[.7] duration-250"
				@click="$emit('delete-task', task.id)"
			>X</button>
		</div>
  </div>
</template>