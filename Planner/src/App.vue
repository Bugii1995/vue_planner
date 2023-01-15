<script>
import { RouterLink, RouterView } from 'vue-router';
import NavBar from './components/NavBar.vue';

export default {
  components: {
    RouterLink,
    RouterView,
    NavBar,
  },
};
</script>

<template>
  <NavBar />
  <RouterView />
</template>
