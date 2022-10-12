<template>
  <div class="flex flex-col mx-auto w-[1200px] items-center">
    <input class="mb-9 ml-3" type="file" @change="loadImage($event)" accept="image/*" />
    <!-- 模擬 lightbox -->
    <div class="w-[600px]" v-if="customImage">
      <crop-box :customImage="customImage" @getCrop="getCrop" />
    </div>

    <div class="h-[300px] w-[300px]">
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
    };
  },
};
</script>

<style lang="scss"></style>
