<template>
  <div class="flex flex-col h-screen w-screen justify-center items-center gap-20">
    <div class="h-[20vh] w-[20vw] overflow-hidden">
      <LineChart v-if="newData" :data="newData" :options="options" />
    </div>
    <div class="h-[20vh] w-[20vw] overflow-hidden">
      <BarChart v-if="newData" :data="newData" :options="options" />
    </div>
    <div class="h-[20vh] w-[20vw] overflow-hidden">
      <PieChart v-if="newData" :data="newData" :options="options" />
    </div>
  </div>
</template>

<script setup>
import axios from 'axios'

import { ref, onMounted } from 'vue'

import BarChart from '@/components/BarChart.vue'
import LineChart from '@/components/LineChart.vue'
import PieChart from '@/components/PieChart.vue'

// const cars = ref(null)

const newData = ref(null)

// const data = ref({
//   labels: ['January', 'February', 'March'],
//   datasets: [{ data: [40, 20, 12], backgroundColor: ['#45322E', '#4C9141', '#497E76'] }]
// })
const options = ref({
  responsive: true,
  plugins: {
    legend: {
      display: false
    }
  }
})

const fetchData = async () => {
  try {
    const { data } = await axios.get('https://mocki.io/v1/e242713d-a765-4a02-8b4e-452f448d97cb')

    const rawLabels = data.map((e) => e.brand)
    const rawSales = data.map((e) => e.sales)

    newData.value = {
      labels: rawLabels,
      datasets: [{ data: rawSales, label: 'Data Pertama' }]
    }
  } catch (e) {
    console.log(e)
  }
}

onMounted(() => {
  fetchData()
})
</script>
