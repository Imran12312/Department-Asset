<template>
  <div class="p-4">
    <h2 class="text-2xl font-bold mb-4">Department Asset List</h2>

    <table class="w-full border mb-4">
      <thead class="bg-gray-300">
        <tr>
          <th class="border p-2">Asset Name</th>
          <th class="border p-2">Department Name</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in assets" :key="index">
          <td class="border p-2 text-center">{{ item.name }}</td>
          <td class="border p-2 text-center">{{ item.department }}</td>
        </tr>
      </tbody>
    </table>

    <div class="flex justify-end">
        <button
        @click="downloadCSV"
        class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700"
        >
        Download CSV File
        </button>
    </div>


  </div>
</template>

<script setup>
import { ref } from 'vue'

// Can replace this with db for proper datanization
const assets = ref([
  { name: 'Printer', department: 'HR' },
  { name: 'Monitor', department: 'IT' },
  { name: 'You 🫵', department: 'COMPANY' },
  { name: 'Barcode Scanner', department: 'ACCOUNT' },

])

// Better in controller -> must be CSV format
const downloadCSV = () => {
  const header = 'Asset Name,Department\n'
  const rows = assets.value.map(a => `${a.name},${a.department}`).join('\n')
  const blob = new Blob([header + rows], { type: 'text/csv' })
  const url = URL.createObjectURL(blob)
  const a = document.createElement('a')
  a.href = url
  a.download = 'assets.csv'
  a.click()
  URL.revokeObjectURL(url)
}
</script>
