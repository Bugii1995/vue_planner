<template>
  <nav
    class="w-fill h-16 mb-16 bg-slate-200 flex justify-center items-center gap-6 shadow-lg text-2xl text-gray-900 font-bold"
  >
    <router-link class="p-4 border-b-4" :to="{ name: 'home' }"
      >Tasks</router-link
    >
    <router-link class="p-4 border-b-4" :to="{ name: 'AddProject' }"
      >Add Task</router-link
    >
  </nav>
</template>
<script>
export default {};
</script>
<style scoped>
a.router-link-active {
  border-bottom: 4px solid black;
}
</style>
