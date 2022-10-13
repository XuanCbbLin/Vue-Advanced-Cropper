<template>
  <div>
    <input class="mb-9" type="file" @change="loadImage($event)" accept="image/*" />
    <!-- 模擬 lightbox -->
    <div v-if="customImage">
      <crop-box :customImage="customImage" :cropWrapperWidth="cropWrapperWidth" @getCrop="getCrop" />
    </div>

    <div class="">
      <img :src="croppedImg" />
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const customImage = ref('');
    const croppedImg = ref('');
    const cropWrapperWidth = 800;

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

    const getCrop = cropImgUrl => {
      croppedImg.value = cropImgUrl;
    };

    return {
      customImage,
      croppedImg,
      loadImage,
      getCrop,
      cropWrapperWidth,
    };
  },
};
</script>

<style lang="scss"></style>
