<template>
  <div class="project" :class="{complete: project.completed}">
      <div class="actions">
          <h3 @click="toggleDetails"> {{ project.title }}</h3>
          <div class="icons">
              <router-link :to="{name: 'EditProject', params: {id: project.id}}">
                <span class="material-icons">edit</span>
              </router-link>
              <span class="material-icons" @click="deleteProject">delete</span>
              <span class="material-icons tick" @click="toggleComplete">done</span>
          </div>
      </div>
        <div class="description">
                <p v-if="showDetails">{{ project.description }}</p>
        </div>
  </div>

</template>

<script>
export default {
props: ['project'],
data() {
        return {
            showDetails: false,
            uri: 'http://localhost:3000/projects/' + this.project.id
        }
    },
methods: {
    // * toggle paragraph visibility
    toggleDetails() {
        this.showDetails = !this.showDetails;
    },
    // ! delete project
    deleteProject() {
        fetch(this.uri, {
            method: 'DELETE'
        })
        .then(response => response.json())
        .then(data => {
            this.$emit('delete-project', this.project.id);
        })
        .catch(error => console.log(error))
    },
    // * toggle project completion
    toggleComplete() {
        fetch(this.uri, {
            method: 'PATCH',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                completed: !this.project.completed
            })
        })
        .then(() => {
            this.$emit('toggle-complete', this.project.id);
        })
        .catch(error => console.log(error))
    }
},
}
</script>

<style>
.project {
  margin: 20px auto;
  max-width: 600px;
  background: #fff;
  padding: 20px;
  border-radius: 4px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
  border-left: 4px solid #e90074;
}
h3 {
  font-size: 1.5em;
  margin: 0;
  padding: 0;
  cursor: pointer;
}

.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.material-icons {
  font-size: 1.5em;
  cursor: pointer;
  margin-left: 10px;
  color: #bbb;
}

.material-icons:hover {
  color: #e90074;
}

.project.complete {
    border-left: 4px solid #4caf50;
}

.project.complete .tick {
    color: #4caf50;
}
</style>