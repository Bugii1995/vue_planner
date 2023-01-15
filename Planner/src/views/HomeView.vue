<template>
  <main class="w-full items-center flex justify-center">
    <div class="w-6/12 rounded text-gray-700 font-bold p-4 h-fit">
      <FilterNav @updateFilter="current = $event" :current="current" />
      <div v-if="projects.length">
        <div v-for="project in filterProjects" :key="project.id">
          <SingleProject
            :project="project"
            @delete="deleteProject"
            @completed="handleCompleted"
            @important="handleImportant"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import SingleProject from '../components/SingleProject.vue';
import FilterNav from '../components/FilterNav.vue';
export default {
  name: 'HomeView',
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all',
    };
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err));
  },
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleCompleted(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.completed = !p.completed;
    },
    handleImportant(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.important = !p.important;
    },
  },
  computed: {
    filterProjects() {
      if (this.current === 'completed') {
        return this.projects.filter((project) => project.completed);
      } else if (this.current === 'ongoing') {
        return this.projects.filter((project) => !project.completed);
      }
      return this.projects;
    },
  },
};
</script>
