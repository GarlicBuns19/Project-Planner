<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id">
      <!-- <p>{{project.title}}</p> -->
      <SingleProject :project="project" @delete="handleDelete" />
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
export default {
  components: { SingleProject },
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((p) => p.id !== id);
      fetch("http://localhost:3000/projects")
        .then((res) => res.json())
        .then((data) => (this.projects = data));
    },
  },
};
</script>
