<template>
  <h2>Add a Project</h2>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input type="text" v-model="title" required />
    <label>Details</label>
    <textarea
      name=""
      id=""
      cols="30"
      rows="10"
      v-model="details"
      required
    ></textarea>
    <br />
    <button @click="addProject">Add project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      details: "",
    };
  },
  methods: {
    handleSubmit() {
      console.log(this.title, ",", this.details);
    },
    addProject() {
      let project = {
        title: this.title,
        details: this.details,
        complete: false,
      };
    //   console.log(project)
      fetch('http://localhost:3000/projects', {
        method: "POST",
        body: JSON.stringify(project),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      }).then(() => {
        this.$router.push('/')
      }).catch(err => {console.log(err)})
      
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:ital@1&display=swap");

form {
  display: flex;
  flex-direction: column;
  /* align-items: center; */
  justify-content: center;
  padding: 10px;
  background: rgba(1, 1, 1, 0.7);
}
label {
  /* padding: 10px; */
  font-size: 20px;
  margin: 3px 0 0 3px;
}
input {
  font-family: "Raleway", sans-serif;
  font-size: 15px;
  padding: 10px;
  margin: 3px;
  color: #feeffe;
  background: transparent;
}
textarea {
  font-family: "Raleway", sans-serif;
  font-size: 15px;
  padding: 10px;
  margin: 3px;
  color: #feeffe;
  background: transparent;
}
button {
  border: 2px solid #efefef;
  padding: 5px;
  align-self: center;
  width: 170px;
  color: #feeffe;
  background: transparent;
}
</style>