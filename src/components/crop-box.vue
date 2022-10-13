<template>
  <div :style="{ width: `${cropWrapperWidth}px` }" class="overflow-hidden">
    <Cropper class="mb-4" ref="cropperBox" :src="customImage" :stencil-component="CircleStencil" />
    <div class="flex mb-5 justify-center">
      <button class="bg-dark-700 text-white py-2 px-2" @click="checkCrop">確定</button>
    </div>
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
      default: '',
    },
    cropWrapperWidth: {
      type: Number,
      default: 600,
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
