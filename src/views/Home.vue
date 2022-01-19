<template>
  <div class="home" >
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <ProjectDetail :project="project" @delete="deleteProject" @complete="completeProject" />
      </div>
    </div>

  </div>
</template>

<script>
import ProjectDetail from '../components/ProjectDetail.vue'


export default {
  name: 'Home',
  components: { ProjectDetail },
  data() {
    return {
      projects: []
    }
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err.message))
  }, 
  methods: {
    deleteProject(id) {
      this.projects = this.projects.filter(project => {
        return project.id !== id
      })
    },
    completeProject(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  }
}
</script>
