<script setup>
import { ref } from 'vue'

const inputUrl = ref('');
const outputUrl = ref('');

const encode = () => {
  outputUrl.value = encodeURIComponent(inputUrl.value);
};

const decode = () => {
  outputUrl.value = decodeURIComponent(inputUrl.value);
}
</script>

<template>
  <div>
    <div class="container text-center" style="padding-top: 120px;">
      <div class="row">
        <div class="col-6 offset-3">
          <ToolInput v-model:input-value="inputUrl"/>
        </div>
      </div>
      <div class="row mt-3 gx-2">
        <div class="col-3 offset-3">
          <button class="btn btn-primary" @click="encode">Encode URL</button>
        </div>
        <div class="col-3">
          <button class="btn btn-warning" @click="decode">Decode URL</button>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col-6 offset-3">
          <ToolOutput :output-value="outputUrl"/>
        </div>
      </div>
    </div>
  </div>
</template>