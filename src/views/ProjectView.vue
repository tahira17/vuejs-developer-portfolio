<template>
  <p class="text-center mb-3 dark:text-purple-300">
    Projects from <font-awesome-icon icon="fa-brands fa-github" />
  </p>
  <div class="max-h-[50vh] overflow-auto sm:w-4/12 mx-auto">
    <Loader v-if="loading" />
    <div v-if="error" class="text-red-500 text-center">{{ error }}</div>
    <div v-for="(project, index) in projects" :key="project.id">
      <a :href="project.html_url" target="_bl">
        <div class="bg-purple-300 mb-4 p-2 rounded-md shadow-md">
          <h2 class="font-bold text-xl">
            {{ ++index }} . {{ formatRepoName(project.name) }}
          </h2>
          <p>{{ project.description }}</p>
        </div>
      </a>
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";
import Loader from "../components/Loader.vue";

const projects = ref([]);
const loading = ref(false);
const error = ref(null);

onMounted(async () => {
  const projectOrder = [
    "reactjs-saas-landing-page",
    "reactjs-curly-hair-care-app",
    "vuejs-responsive-website",
    "reactjs-developer-portfolio",
    "reactjs-movie-explorer",
    "reactjs-calculator-app",
  ];

  loading.value = true;

  try {
    const res = await fetch("https://api.github.com/users/tahira17/repos");

    if (!res.ok) throw new Error("Failed to fetch repositories");

    const repos = await res.json();

    projects.value = projectOrder
      .map((name) => repos.find((repo) => repo.name === name))
      .filter(Boolean);
  } catch (ex) {
    error.value = ex.message;
  } finally {
    loading.value = false;
  }
});

const formatRepoName = (name) => {
  return name.replace(/-/g, " ").replace(/\b\w/g, (char) => char.toUpperCase());
};
</script>
