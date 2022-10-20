<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{name : 'edit', params :{ id : project.id}}">
            <span class="material-icons"> edit </span>
        </router-link>
        <span class="material-icons" @click="deleteProject"> delete </span>
        <span class="material-icons tick" @click="tickProject"> done </span>
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
        .then(() => {
          this.$emit("delete", this.project.id);
        })
        .catch((err) => console.log(err));
    },
    tickProject() {
      fetch(this.url, {
        method: "PATCH",
        body: JSON.stringify({
          complete: !this.project.complete,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then(() => this.$emit("tickTask", this.project.id))
        .catch((err) => console.log(err));
    }
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

.complete
    border-left: 4px solid #158519
    .actions
        .icons
            .tick
                color: #158519
</style>
