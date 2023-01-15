<template>
  <div
    :class="{ 'bg-green-200 border-l-green-700': project.completed }"
    class="border-l-red-400 py-6 mb-6 text-2xl border-l-4 border-l-solid px-4 bg-slate-200 shadow-xl rounded flex flex-col justify-center"
  >
    <div class="flex justify-between w-full items-center">
      <div class="cursor-pointer flex gap-2">
        <div @click="show = !show">{{ project.title }}</div>
        <div @click="toggleImportant" v-if="project.important">🌭</div>
        <div @click="toggleImportant" class="opacity-25" v-else>🌭</div>
      </div>
      <div class="flex gap-2">
        <div
          :class="{ 'opacity-100': project.completed }"
          class="cursor-defaulthover:opacity-100"
          v-if="project.completed"
          @click="toggleCompleted"
        >
          ✅
        </div>
        <div
          @click="toggleCompleted"
          class="cursor-default opacity-25 hover:opacity-100"
          v-else
        >
          ❌
        </div>
        <div
          @click="handleEdit"
          class="cursor-default opacity-25 hover:opacity-100"
        >
          🖊️
        </div>
        <div
          @click="deleteProject"
          class="cursor-default opacity-25 hover:opacity-100"
        >
          🗑️
        </div>
      </div>
    </div>
    <div v-if="show">
      <p class="font-light text-xl p-2">{{ project.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['project'],
  data() {
    return {
      show: false,
      uri: 'http://localhost:3000/projects/' + this.project.id,
    };
  },
  methods: {
    deleteProject() {
      fetch(this.uri, { method: 'DELETE' })
        .then(() => this.$emit('delete', this.project.id))
        .catch((err) => console.log(err));
    },
    toggleCompleted() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ completed: !this.project.completed }),
      })
        .then(() => this.$emit('completed', this.project.id))
        .catch((err) => console.log(err));
    },
    toggleImportant() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({ important: !this.project.important }),
      })
        .then(() => this.$emit('important', this.project.id))
        .catch((err) => console.log(err));
    },
    handleEdit() {
      console.log(this.$router.push('/projects/' + this.project.id));
      () => this.$router.push('/projects/' + this.project.id);
    },
  },
};
</script>
