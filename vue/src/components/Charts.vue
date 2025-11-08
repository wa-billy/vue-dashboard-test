<template lang="">
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
        <!-- Animate Revanue Line Chart -->
         <div class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5
         dark:backdrop-blur-md dark:[--webkit-backdrop-filter:blur(10px)]
         dark:border-white/20">
            <h2 calss="text-lg font-semibold mb-4">Monthly Revanue</h2>
            <Line :data="revanueChartData" :options="lineChartOptions" class="max-h-[300px]" :key="lineChartKey"/>
         </div>

         <!-- Animated Doughnut Chart -->
          <div class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5 dark:backdrop-blur-md
          dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20"
          >
        <h2 class="text-lg font-semibold mb-4">Revenue Sources</h2>
        <Doughnut :data="doughnutChartData" :options="doughnutOptions" class="max-h-[300px]" :key="doughnutChartKey"/>
        </div>
    </div>
</template>

<script setup>
import { Line, Doughnut } from 'vue-chartjs'
import { ref, onMounted } from 'vue'
import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    LineElement,
    CategoryScale,
    LinearScale,
    PointElement,
    ArcElement
} from 'chart.js'

ChartJS.register([
    Title,
    Tooltip,
    Legend,
    LineElement,
    CategoryScale,
    LinearScale,
    PointElement,
    ArcElement
])

const lineChartKey = ref(0)
const doughnutChartKey = ref(0)


const doughnutChartData = ref({
    labels: ['Products', 'Services', 'Subscriptions', 'Consulting'],
    datasets: [
        {
            data: [12, 19, 30, 50],
            fill: false,
            backgroundColor: ['#463581', '#E82561', '#ECE852', '#FFA24C'],
            borderWidth: 0,
            hoverOffset: 10
        }
    ]
})

const doughnutOptions = ref({
    responsive: true,
    maintainAspectRatio: false,
    cutout: '70%',
    animation: {
        duration: 1000,
        easing: 'easeOutQuart',
        animateScale: true,
        animateRotate: true
    },
    plugins: {
        legend: {
            position: 'right',
            labels: {
                color: '#64748b',
                boxWidth: 12,
                padding: 16
            }
        },
        tooltip: {
            callbacks: {
                label: function (context) {
                    return `${context.label}:${context.raw}`
                }
            }
        }
    }
})

const revanueChartData = ref({
    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun'],
    datasets: [
        {
            data: [1200, 1900, 3000, 5000, 2000, 4000],
            fill: false,
            borderColor: '#E82561',
            backgroundColor: '#E82561',
            tension: 0.4
        }
    ]
})

const lineChartOptions = ref({
    responsive: true,
    maintainAspectRatio: false,
    animation: {
        tension: {
            duration: 1000,
            easing: 'linear',
            from: 1,
            to: 0,
            loop: false
        }
    },
    plugins: {
        legend: {
            labels: {
                color: '#64748b'
            }
        }
    },
    scales: {
        x: {
            grid: {
                color: 'rgba(0,0,0,0.1)'
            }
        },
        y: {
            grid: {
                color: 'rgba(0,0,0,0.1)'
            },
            Ticks: {
                color: '#64748b'
            }
        }
    }
})

onMounted(() => {
    // Force re-ender of charts to trigger animates
    lineChartKey.value++
    doughnutChartKey.value++
})
</script>
