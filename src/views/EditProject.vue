<template>
  <form @submit.prevent="updateProject">
      <label for="">Title</label>
      <input type="text" required v-model="title">
      <label for="">Details:</label>
      <textarea required v-model="description"></textarea>
      <button>Update project</button>
  </form>
</template>

<script>
export default {
props: ['id'],
data () {
    return {
        title: '',
        details: '',
        uri: 'http://localhost:3000/projects/' + this.id
    }
},
mounted() {
    fetch(this.uri)
    .then(response => response.json())
    .then(data => {
        this.title = data.title;
        this.description = data.description;
    })
    .catch(error => console.log(error))
},
methods: {
    updateProject() {
        fetch(this.uri, {
            method: 'PATCH',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                title: this.title,
                description: this.description
            })
        })
        .then(() => {
            this.$router.push('/');
        })
        .catch(error => console.log(error))
    }
}
}
</script>

<style>

</style>