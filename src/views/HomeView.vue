<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current=current />
    <div v-if="filterProjects">
      <div v-for="project in filterProjects" :key="project.id">
      <!-- <div v-for="project in projects" :key="project.id"> -->
        <!-- <p>{{project.title}}</p> -->
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @tickTask="handleTick"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";

export default {
  components: { SingleProject , FilterNav},
  data() {
    return {
      projects: [],
      current : 'all'
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
    handleTick(id) {
      let p = this.projects.find(p => p.id === id)
      p.complete = !p.complete
      fetch("http://localhost:3000/projects")
        .then((res) => res.json())
        .then((data) => (this.projects = data));
    },
  },
  computed : {
    filterProjects(){
      if(this.current === 'completed'){
        return this.projects.filter(p => p.complete)
      }
      if(this.current === 'ongoing'){
        return this.projects.filter(p => !p.complete)
      }
      return this.projects
    }
  }
};
</script>
