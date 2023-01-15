<template>
  <main class="w-full items-center flex justify-center">
    <div class="w-6/12 rounded bg-slate-200 text-2xl shadow-xl p-8 h-fit">
      <form class="flex flex-col gap-6" @submit.prevent="handleUpdate">
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
          Update Task
        </button>
      </form>
    </div>
  </main>
</template>
<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      description: '',
      uri: 'http://localhost:3000/projects/' + this.id,
    };
  },
  methods: {
    handleUpdate() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          title: this.title,
          description: this.description,
        }),
      })
        .then(() => this.$router.push('/'))
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.description = data.description;
      })
      .catch((err) => console.log(err));
  },
};
</script>
