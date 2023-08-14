
<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import Chart from 'chart.js/auto';

const chartCanvas = ref(null);

const data = [
  {
    name: 'Fruits',
    value: 30,
  },
  {
    name: 'Vegetables',
    value: 25,
  },
  {
    name: 'Meat',
    value: 20,
  },
  {
    name: 'Dairy',
    value: 15,
  },
  {
    name: 'Other',
    value: 10,
  },
];

let chartInstance = null;

onMounted(() => {
  if (chartCanvas.value) {
    const ctx = chartCanvas.value.getContext('2d');
    chartInstance = new Chart(ctx, {
      type: 'pie',
      data: {
        labels: data.map(d => d.name),
        datasets: [
          {
            data: data.map(d => d.value),
            backgroundColor: ['#47B39C', '#D52DB7', '#FF2E7E', '#FF6B45', '#FFAB05'],
          },
        ],
      },
      options: {
        plugins: {
            legend: {
                labels: {
                  font: {
                        size: 16,
                        weight:'bold',
                        style:'italic'                                           
                    }
                }
            }
        }
    }
    });
  }
});

onBeforeUnmount(() => {
  if (chartInstance) {
    chartInstance.destroy();
    chartInstance = null;
  }
});
</script>

<template>
   <div class="flex flex-col justify-center text-center text-4xl font-bold text-rose-600 mt-10">
    <div>
      <h1>A Pie Chart of Daily Needs</h1>
    </div>
       
  <div class="w-96 h-96 flex justify-center items-center mt-10 mx-auto">
    <canvas ref="chartCanvas"></canvas>
  </div>
</div>

</template>


<style>

</style>
