<template>
  <div class="home">
    <FilterNav @update-filter="current = $event" :current="current"></FilterNav>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete-project="handleDelete" @toggle-complete="handleComplete"></SingleProject>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
  components: {SingleProject, FilterNav},
  data () {
    return {
      projects: [],
      current: 'all'
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
  },
  computed: {
    filteredProjects() {
      if (this.current === 'all') {
        return this.projects;
      } else if (this.current === 'completed') {
        return this.projects.filter(project => project.completed);
      } else if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.completed);
      }
    }
  }
}
</script>
