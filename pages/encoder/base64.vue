<script setup>
import { ref } from 'vue'

const title = 'Base64';
const inputUrl = ref('');
const outputUrl = ref('');

const encode = () => {
  outputUrl.value = btoa(inputUrl.value);
};

const decode = () => {
  outputUrl.value = atob(inputUrl.value);
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
              <ToolInput v-model:input-value="inputUrl"/>
            </div>
          </div>
          <div class="row mt-3 gx-2">
            <div class="d-grid col-6">
              <button class="btn btn-primary" @click="encode">Encode</button>
            </div>
            <div class="d-grid col-6">
              <button class="btn btn-warning" @click="decode">Decode</button>
            </div>
          </div>
          <div class="row mt-3">
            <div class="col">
              <ToolOutput :output-value="outputUrl"/>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>