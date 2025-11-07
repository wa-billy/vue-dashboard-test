<template>
    <div class="grid grid-cols-1 md:grid-cols4 gap-6 mb-6">
        <div v-for="(stat, index) in statsData" 
        :key="index" 
        class="stats bg-base-100 shadow dark:bg-white/5 dark:backdrop-blur-md 
        dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20">
            <div class="stat">
                <div class="stat-title">{{ stat.title }}</div>
                <div class="stat-value">{{ stat.value }}</div>
                <div class="stat-desc" 
                :class="{
                    'text-green-500': isPositiveChange(stat.desc),
                    'text-red-500': !isPositiveChange(stat.desc)
                }"
                >
                    {{ stat.desc }}
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue'
const statsData = ref([
    { title: 'Total Users', value: '123', desc: '↗ 14% from a month' },
    { title: 'Revanue', value: '456', desc: '↗ 23% from a month' },
    { title: 'New Orders', value: '789', desc: '↗ 34% from a month' },
    { title: 'Active Projects', value: '1234', desc: '↗ 45% from a month' }
])

const isPositiveChange = (desc) => {
    return desc.includes('↗')
}
</script>
