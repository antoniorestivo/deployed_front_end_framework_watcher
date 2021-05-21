<template>
  <div class="home">
    <h1>Frontend Framework Watcher</h1>
    <p>This page tracks the popularity data for 5 popular frontend frameworks</p>
    <div v-if="chartOptions && series">
      <apexchart type="bar" height="350" :options="chartOptions" :series="series"></apexchart>
    </div>
    <div v-if="chartOptions1 && series1">
      <apexchart type="pie" width="380" :options="chartOptions1" :series="series1"></apexchart>
      <p style="float: left">
        Total number of Watchers, Stars, and Forks
        <br />
        for each framework, broken up into a pie chart
      </p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import VueApexCharts from "vue3-apexcharts";

// TODO
// add data below to be rendered to the screen in a chart/graph format
export default {
  components: {
    apexchart: VueApexCharts,
  },
  data: function () {
    return {
      series: [
        {
          name: "Watchers",
          data: [],
        },
        {
          name: "Stargazers",
          data: [],
        },
        {
          name: "Forks",
          data: [],
        },
      ],
      chartOptions: {
        chart: {
          type: "bar",
          height: 350,
          stacked: true,
        },
        plotOptions: {
          bar: {
            horizontal: true,
          },
        },
        stroke: {
          width: 1,
          colors: ["#fff"],
        },
        title: {
          text: "Framework Popularity Data",
        },

        xaxis: {
          categories: [],
          labels: {
            formatter: function (val) {
              return val;
            },
          },
        },
        yaxis: {
          title: {
            text: undefined,
          },
        },
        tooltip: {
          y: {
            formatter: function (val) {
              return val;
            },
          },
        },
        fill: {
          opacity: 1,
        },
        legend: {
          position: "top",
          horizontalAlign: "left",
          offsetX: 40,
        },
      },

      series1: [],
      chartOptions1: null,
      message: "Welcome to Vue.js!",
      data1: "",
      frameworkArray: [],
      vue_subscribers: "",
      vue_stargazers: "",
      vue_forks: "",

      react_subscribers: "",
      react_stargazers: "",
      react_forks: "",

      svelte_subscribers: "",
      svelte_stargazers: "",
      svelte_forks: "",

      ember_subscribers: "",
      ember_stargazers: "",
      ember_forks: "",

      angular_subscribers: "",
      angular_stargazers: "",
      angular_forks: "",
    };
  },
  mounted: function () {
    this.allData();
   
  },
  methods: {
    allData: function () {
      //data where array[i] == "vuejs/stargazers"
      axios.get("https://api.github.com/repos/vuejs/vue").then((vue_response) => {
        axios.get("https://api.github.com/repos/facebook/react").then((react_response) => {
          axios.get("https://api.github.com/repos/angular/angular.js").then((angular_response) => {
            axios.get("https://api.github.com/repos/sveltejs/svelte").then((svelte_response) => {
              axios.get("https://api.github.com/repos/emberjs/ember.js").then((ember_response) => {
                this.data = ember_response.data;
                console.log(this.data);
                console.log("Ember.js");
                console.log("forks:" + ember_response.data.forks_count);
                console.log("stargazers:" + ember_response.data.stargazers_count);
                console.log("subscribers:" + ember_response.data.subscribers_count);
                var whole =
                  ember_response.data.forks_count +
                  ember_response.data.stargazers_count +
                  ember_response.data.subscribers_count;

                this.series1.push(whole);
                this.chartOptions1.labels.push("Ember");
                this.chartOptions.xaxis.categories.push("Ember");
                this.ember_forks = this.series[2].data.push(ember_response.data.forks_count);
                this.ember_subscribers = this.series[1].data.push(ember_response.data.subscribers_count);
                this.ember_stargazers = this.series[0].data.push(ember_response.data.watchers_count);
              });

              this.data = svelte_response.data;
              console.log(this.data);
              console.log("Svelte.js");
              console.log("forks:" + svelte_response.data.forks_count);
              console.log("stargazers:" + svelte_response.data.stargazers_count);
              console.log("subscribers:" + svelte_response.data.subscribers_count);
              var whole =
                svelte_response.data.forks_count +
                svelte_response.data.stargazers_count +
                svelte_response.data.subscribers_count;

              this.series1.push(whole);
              this.chartOptions1.labels.push("Svelte");
              this.chartOptions.xaxis.categories.push("Svelte");
              this.svelte_forks = this.series[2].data.push(svelte_response.data.forks_count);
              this.svelte_subscribers = this.series[1].data.push(svelte_response.data.subscribers_count);
              this.svelte_stargazers = this.series[0].data.push(svelte_response.data.watchers_count);
            });
            this.data = angular_response.data;
            console.log(this.data);
            console.log("Angular.js");
            console.log("forks:" + angular_response.data.forks_count);
            console.log("stargazers:" + angular_response.data.stargazers_count);
            console.log("subscribers:" + angular_response.data.subscribers_count);
            var whole =
              angular_response.data.forks_count +
              angular_response.data.stargazers_count +
              angular_response.data.subscribers_count;

            this.series1.push(whole);
            this.chartOptions1.labels.push("Angular");
            this.chartOptions.xaxis.categories.push("Angular");
            this.angular_forks = this.series[2].data.push(angular_response.data.forks_count);
            this.angular_subscribers = this.series[1].data.push(angular_response.data.subscribers_count);
            this.angular_stargazers = this.series[0].data.push(angular_response.data.watchers_count);
          });

          this.data = react_response.data;
          console.log(this.data);
          console.log(react_response.data.full_name);
          console.log("forks:" + react_response.data.forks_count);
          console.log("stargazers:" + react_response.data.stargazers_count);
          console.log("subscribers:" + react_response.data.subscribers_count);
          var whole =
            react_response.data.forks_count +
            react_response.data.stargazers_count +
            react_response.data.subscribers_count;

          this.series1.push(whole);
          this.chartOptions1.labels.push("React");
          this.chartOptions.xaxis.categories.push("React");
          this.react_forks = this.series[2].data.push(react_response.data.forks_count);
          this.react_subscribers = this.series[1].data.push(react_response.data.subscribers_count);
          this.react_stargazers = this.series[0].data.push(react_response.data.watchers_count);
        });
        this.data = vue_response.data;
        console.log(this.data);
        console.log("Vue.js");
        console.log("forks:" + vue_response.data.forks_count);
        console.log("stargazers:" + vue_response.data.stargazers_count);
        console.log("subscribers:" + vue_response.data.subscribers_count);
        // this.series1 = [vue_response.dataforks, vue_response.datastargazers_count, vue_response.data.subscribers];
        var whole =
          vue_response.data.forks_count + vue_response.data.stargazers_count + vue_response.data.subscribers_count;

        // TODO
        // This data below needs to be manipulated into portions percentages, so we have to figure out how to get each piece of data turned into a percentage of the
        // subscribers for each framework for example, vue subscribers + svelte subscribers + angular subscribers = 334645, then divide each one by that number to get the pie chart percentage
        var forks = whole / vue_response.data.forks_count;
        console.log(forks);
        var stargazers = whole / vue_response.data.stargazers_count;
        console.log(stargazers);

        var subscribers = whole / vue_response.data.subscribers_count;
        console.log(subscribers);

        this.series1.push(whole);
        this.chartOptions.xaxis.categories.push("Vue");
        this.vue_stargazers = this.series[0].data.push(vue_response.data.watchers_count);
        this.vue_subscribers = this.series[1].data.push(vue_response.data.subscribers_count);
        this.vue_forks = this.series[2].data.push(vue_response.data.forks_count);
        // this.series.push(forks, stargazers, subscribers)
        // = [forks, stargazers , subscribers]; //these numbers must add up to 100 to form a percentage
        this.chartOptions1 = {
          chart: {
            width: 380,
            type: "pie",
          },
          labels: ["Vue"],
          responsive: [
            {
              breakpoint: 480,
              options: {
                chart: {
                  width: 200,
                },
                legend: {
                  position: "bottom",
                },
              },
            },
          ],
        };
      });
    },
  },
};
</script>
