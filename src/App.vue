<template>
  <input class="mb-9 ml-3" type="file" @change="loadImage($event)" accept="image/*" />
  <!-- 模擬 lightbox -->
  <div class="w-[600px]" v-if="customImage">
    <crop-box :customImage="customImage" />
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const customImage = ref('');

    const loadImage = event => {
      const { files } = event.target;

      if (files?.[0]) {
        const reader = new FileReader();

        reader.readAsDataURL(files[0]);

        reader.addEventListener('load', event => {
          customImage.value = event.target.result;
        });
      }
    };

    return {
      customImage,
      loadImage,
    };
  },
};
</script>

<style lang="scss"></style>
