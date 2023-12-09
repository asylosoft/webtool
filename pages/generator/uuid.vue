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
  <div class="container-fluid">
    <div class="row">
      <div class="col col-sm-10 offset-sm-1 col-md-8 offset-md-2 col-lg-6 offset-lg-3 col-xl-4 offset-xl-4">

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

      </div>
    </div>
  </div>
</template>