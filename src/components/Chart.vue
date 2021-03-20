<template>
    <pie-chart v-for="repo in repos" :key="repo.id"  :data="repo.contributions" :options="chartOptions"></pie-chart>
   <h2 v-for="repo in repos" :key="repo.id"  >{{repo.contributions}}</h2>
</template>
<script>
import axios from "axios"
import { Doughnut, mixins } from "vue-chartjs";
import PieChart from "./PieChart.js";
export default {
   name : "Chart",
   data(){
       return {
           repos : null,
           extends: Doughnut,
           
            chartOptions: {
        hoverBorderWidth: 20
      },
      chartData: {
        hoverBackgroundColor: "red",
        hoverBorderWidth: 10,
        labels: ["Green", "Red", "Blue"],
        datasets: [
          {
            label: "Data One",
            backgroundColor: ["#41B883", "#E46651", "#00D8FF"],
            data: [1, 10, 5]
          }
        ]
      }
    };
       },
     created: function () {
    axios.get("https://api.github.com/repos/Dibyadarshidas/30-Days-Of-React/contributors").then((response) => {
      this.repos = response.data;
    });
  } 
}
</script>
