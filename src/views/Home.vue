<template>
  <div class="home">
    <div>
      <h1>Stars:</h1>
      <h4>vue stars: {{ vue_stats.stargazers_count }}</h4>
      <h4>angular stars: {{ angular_stats.stargazers_count }}</h4>
      <h4>ember stars: {{ ember_stats.stargazers_count }}</h4>
      <h4>svelte stars: {{ svelte_stats.stargazers_count }}</h4>
      <h4>react stars: {{ react_stats.stargazers_count }}</h4>
    </div>
    <div>
      <h1>Watches:</h1>
      <h4>vue watches: {{ vue_stats.watchers_count }}</h4>
      <h4>angular watches: {{ angular_stats.watchers_count }}</h4>
      <h4>ember watches: {{ ember_stats.watchers_count }}</h4>
      <h4>svelte watches: {{ svelte_stats.watchers_count }}</h4>
      <h4>react watches: {{ react_stats.watchers_count }}</h4>
    </div>
    <div>
      <h1>Forks:</h1>
      <h4>vue forks: {{ vue_stats.forks }}</h4>
      <h4>angular forks: {{ angular_stats.forks }}</h4>
      <h4>ember forks: {{ ember_stats.forks }}</h4>
      <h4>svelte forks: {{ svelte_stats.forks }}</h4>
      <h4>react forks: {{ react_stats.forks }}</h4>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      vue_stats: {},
      angular_stats: {},
      ember_stats: {},
      svelte_stats: {},
      react_stats: {},
    };
  },
  created: function () {
    this.vueStats();
    this.angularStats();
    this.emberStats();
    this.svelteStats();
    this.reactStats();
  },
  methods: {
    vueStats: function () {
      axios.get("https://api.github.com/repos/vuejs/vue").then((response) => {
        console.log(response.data);
        this.vue_stats = response.data;
      });
    },
    angularStats: function () {
      axios
        .get("https://api.github.com/repos/angular/angular.js")
        .then((response) => {
          console.log(response.data);
          this.angular_stats = response.data;
        });
    },
    emberStats: function () {
      axios
        .get("https://api.github.com/repos/emberjs/ember.js")
        .then((response) => {
          console.log(response.data);
          this.ember_stats = response.data;
        });
    },
    svelteStats: function () {
      axios
        .get("https://api.github.com/repos/sveltejs/svelte")
        .then((response) => {
          console.log(response.data);
          this.svelte_stats = response.data;
        });
    },
    reactStats: function () {
      axios
        .get("https://api.github.com/repos/facebook/react")
        .then((response) => {
          console.log(response.data);
          this.react_stats = response.data;
        });
    },
  },
};
</script>
