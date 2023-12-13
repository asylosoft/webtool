<script setup lang="ts">
import { uuid } from 'vue-uuid'
import { ref } from 'vue'

const title = 'UUID';

const newUuidV4 = ref(uuid.v4());

const generateUuidV4 = () => {
  newUuidV4.value = uuid.v4();
}
</script>

<template>
  <ToolContainer>
    <PageHeader :title="title" />
    <div class="container-fluid text-center">
      <div class="row">
        <div class="col">
          <ToolOutput :output-value="newUuidV4"/>
        </div>
      </div>
      <div class="row mt-3">
        <div class="d-grid">
          <button class="btn btn-primary" @click="generateUuidV4">Generate UUIDv4</button>
        </div>
      </div>
    </div>
  </ToolContainer>
</template>