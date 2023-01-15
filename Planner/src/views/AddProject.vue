<template>
  <main class="w-full items-center flex justify-center">
    <div class="w-6/12 rounded bg-slate-200 text-2xl shadow-xl p-8 h-fit">
      <form class="flex flex-col gap-6" @submit.prevent="handleSubmit">
        <label class="text-gray-700 font-bold">Title:</label>
        <input class="rounded p-4" type="text" v-model="title" required />
        <label class="text-gray-700 font-bold">Description:</label>
        <textarea
          class="rounded h-36 p-4"
          v-model="description"
          required
        ></textarea>

        <button
          class="bg-green-300 text-gray-00 font-bold m-auto rounded hover:bg-green-900 hover:text-white p-4 w-fit"
        >
          Add Task
        </button>
      </form>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      description: '',
    };
  },
  methods: {
    handleSubmit() {
      console.log(this.title, this.description, this.important);
      let project = {
        title: this.title,
        description: this.description,
        important: this.important,
        completed: false,
      };
      fetch('http://localhost:3000/projects', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(project),
      })
        .then(() => this.$router.push('/'))
        .catch((err) => console.log(err));
    },
  },
};
</script>
