<script setup lang="ts">
import { uuid } from 'vue-uuid'
import { ref } from 'vue'

const newUuidV4 = ref(uuid.v4());

const generateUuidV4 = () => {
  newUuidV4.value = uuid.v4();
}
</script>

<template>
  <div class="container text-center" style="padding-top: 120px;">
    <div class="row">
      <div class="col-6 offset-3">
        <ToolOutput :output-value="newUuidV4"/>
      </div>
    </div>
    <div class="row mt-3">
      <div class="d-grid col-4 offset-4">
        <button class="btn btn-primary" @click="generateUuidV4">Generate UUIDv4</button>
      </div>
    </div>
  </div>
</template>