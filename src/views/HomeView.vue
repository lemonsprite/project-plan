<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @done="handleDone"></SingleProject>
      </div>
    </div>
  </div>

</template>

<script>
import SingleProject from '@/components/SingleProject.vue'

export default {
  name: 'HomeView',
  components: {
    SingleProject
  },
  data() {
    return {
      projects: [],
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((p) => {
        return p.id !== id
      })
    },
    handleDone(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })

      p.complete = !p.complete
    }
  }
}
</script>
