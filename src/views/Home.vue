<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete-project="handleDelete" @toggle-complete="handleComplete"></SingleProject>
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
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(project => project.id !== id);
    },
    handleComplete(id) {
      this.projects = this.projects.map(project => {
        if (project.id === id) {
          project.completed = !project.completed;
        }
        return project;
      });
    }
  }
}
</script>
