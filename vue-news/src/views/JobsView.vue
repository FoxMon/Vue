<template>
<div>
  <div v-for="job in jobs" v-bind:key="job.id">{{ job.title }}</div>
</div>
</template>
<script>

import { fetchJobsList } from '../api/index.js';

export default {
  data() {
    return {
      jobs: [],
    }
  },
  created() {
    fetchJobsList()
      .then(response => this.jobs = response.data)
      .catch(e => console.log(e));
  }
}
</script>
<style>
</style>
