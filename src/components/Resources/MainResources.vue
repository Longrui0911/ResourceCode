<template>
  <div class="main-resources">
    <div class="tabs">
      <button
        :class="{ active: isActiveStore }"
        @click="currentTab = 'StoreResources'"
      >
        Store Resources
      </button>
      <button
        :class="{ active: isActiveAdd }"
        @click="currentTab = 'AddResources'"
      >
        Add Resoures
      </button>
    </div>
  </div>

  <component :is="currentTab" :resources="resources"></component>
</template>

<script>
import AddResources from "./AddResources.vue";
import StoreResources from "./StoreResources.vue";

export default {
  name: "MainResources",
  components: {
    AddResources,
    StoreResources,
  },
  provide() {
    return {
      addResources: this.addResources,
      deleteResources: this.deleteResources,
    };
  },
  data() {
    return {
      currentTab: "StoreResources",
      resources: [],
    };
  },
  methods: {
    getLocalStorage(name) {
      return JSON.parse(localStorage.getItem(name));
    },
    setLocalStorage(name, data) {
      localStorage.setItem(name, JSON.stringify(data));
    },
    addResources(title, description, link) {
      const newCourse = { title: title, description: description, link: link };
      this.resources.push(newCourse);
      this.setLocalStorage("resources", this.resources);
      this.resources = this.getLocalStorage("resources");
      this.currentTab = "StoreResources";
    },

    deleteResources(index) {
      this.resources = JSON.parse(localStorage.resources);
      this.resources.splice(index, 1);
    },
  },
  computed: {
    isActiveStore() {
      if (this.currentTab == "TabStore") {
        return true;
      } else {
        return false;
      }
    },
    isActiveAdd() {
      if (this.currentTab == "TabAdd") {
        return true;
      } else {
        return false;
      }
    },
  },
  watch: {
    resources: {
      handler(newCourses) {
        localStorage.resources = JSON.stringify(newCourses);
      },
      deep: true,
    },
  },
  mounted() {
    if (localStorage.resources) {
      this.resources = JSON.parse(localStorage.resources);
    }
    const resources = this.getLocalStorage("resources");
    if (resources.length) {
      this.resources = resources;
    } else {
      this.setLocalStorage("resources", []);
    }
  },
};
</script>

<style scoped>
.main-resources {
  max-width: 40rem;
  margin: 0 auto;
}
.tabs {
  border-radius: 12px;
  box-shadow: 0 2px 8px rgb(0 0 0 / 26%);
  padding: 1rem;
  margin: 2rem auto;
  max-width: 40rem;
}
</style>