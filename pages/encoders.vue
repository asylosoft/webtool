<script setup lang="ts">
const tools = [
  {
    title: "URL",
    description: "Encode/decode URL",
    url: "encoder/url"
  },
]
</script>

<template>
  <div class="container text-center">
    <div class="row">
      <div class="col col-md-3" v-for="tool in tools">
        
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ tool.title }}</h5>
            <NuxtLink :to="tool.url" class="stretched-link"></NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>