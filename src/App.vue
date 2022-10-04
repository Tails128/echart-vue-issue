<script setup lang="ts">
import { ref, watch } from "vue";
import * as echarts from "echarts";
import { useWindowSize } from "@vueuse/core";

const option = {
  xAxis: {
    type: "category",
    data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
  },
  yAxis: {
    type: "value",
  },
  series: [
    {
      data: [150, 230, 224, 218, 135, 147, 260],
      type: "line",
    },
  ],
};

const chart = ref();
const graphRef = ref(null);
watch(graphRef, () => makeGraph());

const { width } = useWindowSize();
watch(width, () => {
  if (chart.value != undefined) {
    console.log("Trying to resize!");
    chart.value.resize();
  }
});

const makeGraph = () => {
  if (graphRef.value == undefined) {
    console.log("I don't exist!");
    return;
  }

  if (chart.value == undefined) {
    chart.value = echarts.init(graphRef.value);
  }

  console.log("Graph created!");
  chart.value.setOption(option);
};
</script>

<template>
  <div
    style="
      width: 100vw;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-items: center;
    "
  >
    <div id="graph" ref="graphRef" style="width: 100%; height: 300px" />
  </div>
</template>
