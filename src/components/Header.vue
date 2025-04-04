<script setup>
  defineEmits(['toggle-night-mode'])
</script>

<template>
  <div class="flex justify-end">
    <i 
      class="fa-solid fa-moon w-fit text-indigo-900 dark:text-white cursor-pointer bg-white dark:bg-indigo-950 px-3 p-2 rounded hover:opacity-[.7] duration-250 border-1 border-slate-400"
      @click="$emit('toggle-night-mode')"
    ></i>
  </div>

  <h1 class="text-3xl text-center my-10 font-bold text-gray-700 dark:text-white ">ToDo List <br>
    <span class="text-lime-600">Vue</span> +
    <span class="text-cyan-400">Tailwind</span>
  </h1>
</template>