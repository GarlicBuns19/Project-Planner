<template>
  <div class="project">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <span class="material-icons"> edit </span>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <span class="material-icons"> done </span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      url: `http://localhost:3000/projects/${this.project.id}`,
    };
  },
  methods: {
    deleteProject() {
      fetch(this.url, {
        method: "DELETE",
      })
      .then(() => { this.$emit('delete', this.project.id)})
      .catch(err => console.log(err))
    },
  },
};
</script>

<style scoped lang="sass">
.project
    background: rgba(1, 1, 1, 0.6)
    padding: 10px
    margin: 20px auto
    border-left: 4px solid #fc2003
    .actions
        display: flex
        align-items: center
        justify-content: space-between
        h3
            cursor: pointer
        .icons
            .material-icons
                font-size: 24px
                margin: 0 0 0 10px
                color: #efefef
                cursor: pointer
                transition: 0.7s
            .material-icons:hover
                color: grey
</style>
