<template>
  <div class="home" >
    <FilterNav @filterChange="current = $event" :current="current" :projects="projects" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <ProjectDetail :project="project" @delete="deleteProject" @complete="completeProject" />
      </div>
    </div>

  </div>
</template>

<script>
import ProjectDetail from '../components/ProjectDetail.vue'
import FilterNav from '../components/FilterNav.vue'


export default {
  name: 'Home',
  components: { ProjectDetail, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all',
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
    },
    
  },
  computed: {
      filteredProjects() {
        if (this.current === 'completed'){
          return this.projects.filter(project => project.complete)
        }
        if(this.current === 'ongoing'){
          return this.projects.filter(project => !project.complete)
        }
        return this.projects
      }
    }
}
</script>


<style>

</style>