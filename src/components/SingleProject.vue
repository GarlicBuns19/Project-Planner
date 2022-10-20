<template>
  <div class="project">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
    </div>
    <div v-if="showDetails" class="details" >
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data(){
    return {
        showDetails : false
    }
  }
};
</script>

<style scoped lang="sass">
.project
    background: rgba(1, 1, 1, 0.6)
    padding: 10px
    margin: 20px auto
    border-left: 4px solid #fc2003
    .actions
        h3
            cursor: pointer

</style>