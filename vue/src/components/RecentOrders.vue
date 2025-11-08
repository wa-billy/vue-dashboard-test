<template>
    <div class="card bg-base-100 shadow dark:bg-white/5 dark:backdrop-blue-md
    dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/50">
        <div class="card-body">
            <h2 class="card-title">Recent Orders</h2>
            <div class="overflow-x-auto">
                <Table class="table">
                    <thead>
                        <tr>
                            <th>Orders ID</th>
                            <th>Customer</th>
                            <th>Date</th>
                            <th>Amount</th>
                            <th>Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(order, index) in recentOders" :key="index">
                            <td>{{ order.id }}</td>
                            <td>{{ order.customer }}</td>
                            <td>{{ order.date }}</td>
                            <td>{{ order.amount }}</td>
                            <td>
                                <span :class="`badge badge-${getStatusClass(order.status)}`">
                                    {{ order.status }}
                                </span>
                            </td>
                        </tr>
                    </tbody>
                </Table>
            </div>
            <div class="card-actions justify-end mt-4">
                <button class="btn btn-primary">View All</button>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref } from 'vue'

const recentOders = ref([
    {
        id: '1',
        customer: 'Kuy',
        date: '2025-11-9',
        status: 'Complete'
    },
    {
        id: '1',
        customer: 'Kuy',
        date: '2025-11-9',
        status: 'Complete'
    },
    {
        id: '1',
        customer: 'Kuy',
        date: '2025-11-9',
        status: 'Complete'
    }

])

function getStatusClass(status) {
    const statusMap = {
        "Complete":"Success",
        "Pending":"Warning",
        "Cancelled":"error",
    }
    return statusMap || 'neural'
}
</script>
