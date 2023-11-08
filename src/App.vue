<template>
  <div class="flex flex-col h-screen w-screen justify-center items-center gap-20">
    <div class="h-[80vh] w-[80vw] overflow-hidden">
      <BarChart v-if="newData" :data="newData" :options="options" />
    </div>
  </div>
</template>

<script setup>
import axios from 'axios'

import { ref, onMounted } from 'vue'

import BarChart from '@/components/BarChart.vue'

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
  const { data } = await axios.get('/cars_data.json')

  const rawLabels = data.map((e) => e.brand)
  const rawSales = data.map((e) => e.sales)

  newData.value = {
    labels: rawLabels,
    datasets: [{ data: rawSales }]
  }
}

onMounted(() => {
  fetchData()
})
</script>
