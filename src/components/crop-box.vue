<template>
  <Cropper
    class="bg-light-100 mb-4 w-full"
    ref="cropperBox"
    :src="customImage"
    :stencil-component="CircleStencil"
  />
  <div class="flex mb-5 justify-center">
    <button class="bg-dark-700 text-white py-2 px-2" @click="checkCrop">確定</button>
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
  emits: ['getCrop'],
  setup(props, { emit }) {
    const cropperBox = ref(null);

    const checkCrop = () => {
      const { canvas } = cropperBox.value.getResult();
      emit('getCrop', canvas.toDataURL());
    };

    return {
      CircleStencil,
      cropperBox,
      checkCrop,
    };
  },
};
</script>

<style></style>
