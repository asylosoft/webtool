<script setup>
import { ref } from 'vue'

const inputUrl = ref('');
const outputUrl = ref('');
const isCopied = ref(false);

const encode = () => {
  outputUrl.value = encodeURIComponent(inputUrl.value);
};

const decode = () => {
  outputUrl.value = decodeURIComponent(inputUrl.value);
}

const copyOutputUrl = () => {
  if (outputUrl.value) {
    navigator.clipboard.writeText(outputUrl.value).then(() => {
      isCopied.value = true;
      setTimeout(() => isCopied.value = false, 500);
    });
  }  
}
</script>

<template>
  <div>
    <div class="container text-center" style="padding-top: 120px;">
      <div class="row">
        <div class="col-6 offset-3">
          <input type="text" class="text-black text-center form-control border border-secondary" v-model="inputUrl" :title="inputUrl" />
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
          <div class="input-group">
            <input type="text" class="text-black text-center form-control border border-secondary" readonly :value="outputUrl" :title="outputUrl" />
            <button v-if="isCopied" class="btn btn-secondary">Copied</button>
            <button v-else class="btn btn-secondary" @click="copyOutputUrl">Copy</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>