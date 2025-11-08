<template>
    <div class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5
         dark:backdrop-blur-md dark:[--webkit-backdrop-filter:blur(10px)]
         dark:border-white/20 mt-5 mb-6">
        <h2 calss="text-lg font-semibold mb-4">Product Performance by Region</h2>
        <Bar :data="barChartData" :options="barChartOptions" class="max-h-[400px]"/>
    </div>
</template>
<script setup>
import { Bar } from 'vue-chartjs';
import { ref } from 'vue'
import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    LinearScale,
} from 'chart.js'

ChartJS.register([
    Title,
    Tooltip,
    Legend,
    BarElement,
    CategoryScale,
    LinearScale,
])

const barChartData = ref({
    labels: ['Q1', 'Q2', 'Q3', 'Q4'],
    datasets: [
        {
            label: 'South',
            data: [1200, 1900, 3000, 5000],
            backgroundColor: '#E82561',
            stack: 'Region'
        },
        {
            label: 'East',
            data: [1200, 1900, 3000, 6000],
            backgroundColor: 'green',
            stack: 'Region'
        },
        {
            label: 'West',
            data: [1200, 1900, 3000, 5000],
            backgroundColor: 'blue',
            stack: 'Region'
        },
        {
            label: 'North',
            data: [1200, 1900, 3000, 5000],
            backgroundColor: 'yellow',
            stack: 'Region'
        }
    ]
})

const barChartOptions = ref({
    responsive: true,
    maintainAspectRatio: false,
    plugins: {
        title: {
            display: false
        },
        legend: {
            position: 'top',
            labels: {
                color: '#64748b',
                bodyWidth: 12,
                padding: 16,
                usePointStyle: true
            }
        },
        tooltip: {
            callback: {
                afterLabel: function(content) {
                    const total = conext.dataset.data.reduce((a, b) => a+b, 0)
                    const percentage = Math.round((content.raw/total)*100)
                    return `Contribution: ${percentage}%`
                }
            }
        }
    },
    scales: {
        x: {
            stacked: true,
            grid: {
                display: false
            },
            ticks: {
                color: '#6478b'
            }
        },
        y: {
            stacked: true,
            grid: {
                color: 'rgba(0,0,0,0.05)'
            },
            ticks: {
                color: '#64748b',
                callback: function(value) {
                    return '$'+value.toLocaleString()
                }
            }
        }
    }
})
</script>