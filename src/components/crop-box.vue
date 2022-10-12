<template>
  <Cropper
    class="bg-light-100 mb-4 w-full"
    ref="cropperBox"
    :src="customImage"
    :stencil-component="CircleStencil"
  />

  <slide-bar v-model:slideValue.number="slideValue" />

  <div class="flex mb-5 justify-center">
    <button class="bg-dark-700 text-white py-2 px-2" @click="checkCrop">確定</button>
  </div>
</template>

<script>
import { ref, watch } from 'vue';
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
    const slideValue = ref(0);

    const checkCrop = () => {
      const { canvas } = cropperBox.value.getResult();
      emit('getCrop', canvas.toDataURL());
    };

    watch(slideValue, newSlideValue => {
      console.log(newSlideValue);
    });

    return {
      CircleStencil,
      cropperBox,
      checkCrop,
      slideValue,
    };
  },
};
</script>

<style></style>
