<script setup lang="ts">
import { inject } from 'vue'

const toolkit = inject<{
  title: string;
    url: string;
    tools: {
        name: string;
        url: string;
    }[];
}[]>('toolkit');
</script>

<template>
  <div class="container text-center">
    <div class="row">
      <div class="col col-md-3" v-for="category in toolkit">
        
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ category.title }}</h5>
            <NuxtLink :to="category.url" class="stretched-link"></NuxtLink>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>


