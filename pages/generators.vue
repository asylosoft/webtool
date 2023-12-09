<script setup lang="ts">
import { inject } from 'vue'

const title = 'Generators';

const toolkit = inject<{
    title: string;
    url: string;
    tools: {
        name: string;
        url: string;
    }[];
}[]>('toolkit');

const tools = toolkit?.filter((tk) => tk.title == title)[0].tools;
</script>

<template>
  <div class="container">
    <PageHeader :title="title" />
    <div class="text-center">
      <div class="row">
        <div class="col col-md-3" v-for="tool in tools">
          
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">{{ tool.name }}</h5>
              <NuxtLink :to="tool.url" class="stretched-link"></NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>    
  </div>
</template>