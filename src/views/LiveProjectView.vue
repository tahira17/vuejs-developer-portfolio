<template>
  <!-- <p class="text-center mb-3 dark:text-purple-300">Demo for Projects</p> -->

  <div class="max-h-[50vh] overflow-auto sm:w-4/12 mx-auto">
    <div
      v-for="(url, name, index) in demoLinks"
      :key="name"
      class="bg-purple-300 mb-4 p-2 rounded-md shadow-md"
    >
      <a
        :href="url"
        target="_blank"
        rel="noopener noreferrer"
        class="font-bold text-xl"
      >
        {{ ++index }} .
        {{
          name.replace(/-/g, " ").replace(/\b\w/g, (char) => char.toUpperCase())
        }}
      </a>
    </div>
  </div>
</template>

<script setup>
import { demoLinks } from "../assets/DemoLinks";
</script>
