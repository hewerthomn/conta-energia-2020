<template>
  <div>
    <highcharts :options="chartOptions"></highcharts>
  </div>
</template>

<script>
import { Chart } from "highcharts-vue";

export default {
  components: {
    highcharts: Chart
  },
  data() {
    let myData = {
      months: [
        "02/2020",
        "03/2020",
        "04/2020",
        "05/2020",
        "06/2020",
        "07/2020",
        "08/2020",
        "09/2020",
        "10/2020",
        "11/2020",
        "12/2020"
      ],
      totalToPay: [
        252.64,
        266.52,
        282.37,
        245.1,
        220.97,
        189.72,
        152.2,
        177.84,
        284.22
      ],
      consumption: [299, 315, 340, 296, 263, 221, 192, 212, 341],
      kwhPrice: [0.844, 0.846, 0.83, 0.828, 0.759, 0.762, 0.736, 0.738, 0.771]
    };

    return {
      chartOptions: {
        chart: { zoomType: "xy" },
        title: { text: "Boletos de Energia - 2020" },
        xAxis: [
          {
            categories: myData.months,
            crosshair: true
          }
        ],
        plotOptions: {
          series: {
            dataLabels: { enabled: true }
          }
        },
        yAxis: [
          {
            // Primary yAxis
            title: { text: "Preço do Kwh" },
            labels: { format: "R${value}" },
            opposite: true
          },
          {
            // Secondary yAxis
            title: { text: "" },
            labels: { format: "{value}" }
          }
        ],
        tooltip: { shared: true },
        series: [
          {
            type: "column",
            name: "Preço do Kwh",
            data: myData.kwhPrice,
            tooltip: { valuePrefix: "R$" },
            dataLabels: { format: "R${point.y}" }
          },
          {
            yAxis: 1,
            type: "column",
            name: "Consumo (kWh)",
            data: myData.consumption,
            tooltip: { valueSuffix: " kW" },
            dataLabels: { format: "{point.y} Kwh" }
          },
          {
            yAxis: 1,
            type: "line",
            name: "Valor da conta",
            data: myData.totalToPay,
            tooltip: { valuePrefix: "R$" },
            dataLabels: { format: "R${point.y}" }
          }
        ]
      }
    };
  }
};
</script>

<style></style>
