<template>
  <div class="home">
    <div v-if="projects.length">
      <FilterNav @filter="filterInit = $event" :filterInit="filterInit" />
      <div v-for="project in filteredData" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @done="handleDone"
        ></SingleProject>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "@/components/SingleProject.vue";
import FilterNav from "@/components/FilterNav.vue";

export default {
  name: "HomeView",
  components: {
    SingleProject,
    FilterNav,
  },
  data() {
    return {
      projects: [],
      filterInit: "all",
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((p) => {
        return p.id !== id;
      });
    },
    handleDone(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });

      p.complete = !p.complete;
    },
  },
  computed: {
    filteredData() {
      if(this.filterInit === 'completed') {
        return this.projects.filter((p) => p.complete)
      }

      if(this.filterInit === 'ongoing') {
        return this.projects.filter((p) => !p.complete)
      }
      
      return this.projects
    }
  }
};
</script>
