<script setup>
import { RouterLink } from 'vue-router';
import Job from '@/components/Job.vue'
import { reactive, defineProps, onMounted } from 'vue'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import axios from 'axios'

const state = reactive({
  jobs: [],
  isLoading: true
})

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false
  }
})

onMounted(async () => {
  try {
    const response = await axios.get('/api/jobs')
    state.jobs = response.data
  } catch (error) {
    console.error('Error fetchig jobs', error)
  } finally {
    state.isLoading = false
  }
})
</script>

<template>
  <div class="container-xl lg:container m-auto">
    <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
      Browse Jobs
    </h2>
    <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
      <PulseLoader />
    </div>
    <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <Job v-for="job in state.jobs.slice(0, limit || state.jobs.length)" :key="job.id" :job="job"></Job>
    </div>
  </div>

  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink to="/jobs" class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700">View All
      Jobs</RouterLink>
  </section>
</template>