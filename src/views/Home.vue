<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project"></SingleProject>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'

export default {
  name: 'Home',
  components: {SingleProject},
  data () {
    return {
      projects: []
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(response => response.json())
      .then(data => {
        this.projects = data;
      })
      .catch(error => console.error(error))
  }
}
</script>
