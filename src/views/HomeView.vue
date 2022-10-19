<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id">
      {{project.id}}
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data(){
    return {
      projects : []
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data)
  }
};
</script>
