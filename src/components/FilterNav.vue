<template>
  <nav class="filterNav">
    <button @click="filterBy('all')" :class="{active : current === 'all'}">View all</button>
    <button @click="filterBy('completed')" :class="{active : current === 'completed'}" >Completed</button>
    <button @click="filterBy('ongoing')" :class="{active : current ==='ongoing'}" >Ongoing</button>
  </nav>
</template>

<script>
export default {
    props : ['current'],
    methods : {
        filterBy(by){
            this.$emit('filterChange',by)
        }
    }
};
</script>

<style scoped>
.filterNav button.active {
  border-bottom: 4px solid #42b983;
  padding: 0px 0 10px 0;
  /* color: #42b983; */
}
</style>