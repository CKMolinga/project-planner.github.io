<template>
  <div class="project">
      <div class="actions">
          <h3 @click="toggleDetails"> {{ project.title }}</h3>
          <div class="icons">
              <span class="material-icons">edit</span>
              <span class="material-icons">delete</span>
              <span class="material-icons">done</span>
          </div>
      </div>
        <div class="description">
                <p v-if="showDetails">{{ project.description }}</p>
        </div>
  </div>

</template>

<script>
export default {
    data() {
        return {
            showDetails: false,
        }
    },
props: ['project'],
methods: {
    // toggle paragraph visibility
    toggleDetails() {
        this.showDetails = !this.showDetails;
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
</style>