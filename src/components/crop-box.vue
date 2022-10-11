<template>
  <Cropper
    class="bg-light-100 mb-4 w-full"
    ref="cropperBox"
    :src="customImage"
    :stencil-component="CircleStencil"
  />
  <div class="flex mb-5">
    <square-button @click="getCrop"> 確定 </square-button>
  </div>

  <div class="h-[300px] w-[300px]">
    <img :src="croppedImg" />
  </div>
</template>

<script>
import { ref } from 'vue';
import { Cropper, CircleStencil } from 'vue-advanced-cropper';
import 'vue-advanced-cropper/dist/style.css';

export default {
  components: {
    Cropper,
  },
  props: {
    customImage: {
      type: String,
    },
  },
  setup() {
    const cropperBox = ref(null);
    const croppedImg = ref('');

    const getCrop = () => {
      const { canvas } = cropperBox.value.getResult();
      croppedImg.value = canvas.toDataURL();
    };

    return {
      CircleStencil,
      croppedImg,
      cropperBox,
      getCrop,
    };
  },
};
</script>

<style></style>
