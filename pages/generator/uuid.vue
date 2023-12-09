<script setup lang="ts">
import { uuid } from 'vue-uuid'
import { ref } from 'vue'

const newUuidV4 = ref(uuid.v4());
const isCopied = ref(false);

const generateUuidV4 = () => {
  newUuidV4.value = uuid.v4();
}
const copyUuidV4 = () => {
  if (newUuidV4.value) {
    navigator.clipboard.writeText(newUuidV4.value).then(() => {
      isCopied.value = true;
      setTimeout(() => isCopied.value = false, 500);
    });
  }  
}
</script>

<template>
  <div class="container text-center" style="padding-top: 120px;">
    <div class="row">
      <div class="col-6 offset-3">
        <div class="input-group">
          <input type="text" class="text-black text-center form-control border border-secondary" readonly :value="newUuidV4" :title="newUuidV4" />
          <button v-if="isCopied" class="btn btn-secondary">Copied</button>
          <button v-else class="btn btn-secondary" @click="copyUuidV4">Copy</button>
        </div>        
      </div>
    </div>
    <div class="row mt-3">
      <div class="d-grid col-4 offset-4">
        <button class="btn btn-primary" @click="generateUuidV4">Generate UUIDv4</button>
      </div>
    </div>
  </div>
</template>