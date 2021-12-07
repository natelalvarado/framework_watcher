<template>
  <div id="app">
    <router-view />
    <div class="home">
      <h1>Javascript Framework Watcher</h1>
      <p>
        This Dashboard tracks the stars, watchers, and forks for the following
        Javascript frameworks: Vue, Angular, Ember, Svelte, and React
      </p>
      <chartxkcd-stackedbar :config="config"></chartxkcd-stackedbar>
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<script>
import axios from "axios";
import { chartxkcdStackedbar } from "chart.xkcd-vue";

export default {
  name: "app",

  data: function () {
    return {
      vue_stats: {},
      angular_stats: {},
      ember_stats: {},
      svelte_stats: {},
      react_stats: {},
      config: {
        title: "Javascript Tracker",
        data: {
          labels: ["Vue", "Angular", "Ember", "Svelte", "React"],
          datasets: [
            {
              label: "Stars",
              data: [1, 2, 3, 4, 5],
            },
            { label: "Watchers", data: [1, 2, 2, 1, 1] },
            { label: "Forks", data: [1, 2, 2, 1, 1] },
          ],
        },
        options: {
          showLegend: true,
          dotSize: 0.8,
          showLabels: true,
          legendPosition: 2,
        },
      },
    };
  },
  components: {
    "chartxkcd-stackedbar": chartxkcdStackedbar,
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
      return axios
        .get("https://api.github.com/repos/vuejs/vue")
        .then((response) => {
          console.log(response.data);
          this.vue_stats = response.data;
          this.config.data.datasets[0].data[0] = response.data.stargazers_count;
          this.config.data.datasets[1].data[0] = response.data.watchers_count;
          this.config.data.datasets[2].data[0] = response.data.forks;
          return response.data;
        });
    },
    angularStats: function () {
      axios
        .get("https://api.github.com/repos/angular/angular.js")
        .then((response) => {
          console.log(response.data);
          this.angular_stats = response.data;
          this.config.data.datasets[0].data[1] = [
            response.data.stargazers_count,
          ];
          this.config.data.datasets[1].data[1] = [response.data.watchers_count];
          this.config.data.datasets[2].data[1] = [response.data.forks];
        });
    },
    emberStats: function () {
      axios
        .get("https://api.github.com/repos/emberjs/ember.js")
        .then((response) => {
          console.log(response.data);
          this.ember_stats = response.data;
          this.config.data.datasets[0].data[2] = [
            response.data.stargazers_count,
          ];
          this.config.data.datasets[1].data[2] = [response.data.watchers_count];
          this.config.data.datasets[2].data[2] = [response.data.forks];
        });
    },
    svelteStats: function () {
      axios
        .get("https://api.github.com/repos/sveltejs/svelte")
        .then((response) => {
          console.log(response.data);
          this.svelte_stats = response.data;
          this.config.data.datasets[0].data[3] = [
            response.data.stargazers_count,
          ];
          this.config.data.datasets[1].data[3] = [response.data.watchers_count];
          this.config.data.datasets[2].data[3] = [response.data.forks];
        });
    },
    reactStats: function () {
      axios
        .get("https://api.github.com/repos/facebook/react")
        .then((response) => {
          console.log(response.data);
          this.react_stats = response.data;
          this.config.data.datasets[0].data[4] = [
            response.data.stargazers_count,
          ];
          this.config.data.datasets[1].data[4] = [response.data.watchers_count];
          this.config.data.datasets[2].data[4] = [response.data.forks];
        });
    },
  },
};
</script>
