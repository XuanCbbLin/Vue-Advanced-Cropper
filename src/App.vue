<template>
  <div class="flex">
    <div>
      <Cropper
        class="bg-light-100 h-[800px] mb-4 w-[1000px]"
        ref="cropperBox"
        :src="img"
        :stencil-component="CircleStencil"
      />
      <div class="flex ml-5">
        <SquareButton @click="getCrop"> 裁切圖片 </SquareButton>
        <SquareButton @click="zoom(2)"> 放大 </SquareButton>
        <SquareButton @click="zoom(0.5)"> 縮小 </SquareButton>
        <SquareButton @click="resetCropper"> 取消 </SquareButton>
        <input class="ml-3" type="file" @change="loadImage($event)" accept="image/*" />
      </div>
    </div>
    <div class="rounded-full h-[300px] ml-8 w-[300px] overflow-hidden">
      <img :src="croppedImg" v-if="croppedImg" />
      <div class="bg-dark-500 h-[300px] w-full" v-else></div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { Cropper, CircleStencil } from 'vue-advanced-cropper';
import SquareButton from './components/square-button.vue';
import 'vue-advanced-cropper/dist/style.css';
import img2 from '../public/berserk.jpeg';

export default {
  components: {
    Cropper,
    SquareButton,
  },
  setup() {
    const img = ref(
      'https://images.unsplash.com/photo-1600984575359-310ae7b6bdf2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=700&q=80'
    );

    const cropperBox = ref(null);
    const croppedImg = ref('');

    const getCrop = () => {
      const { canvas } = cropperBox.value.getResult();

      croppedImg.value = canvas.toDataURL();
    };

    const zoom = factor => {
      cropperBox.value.zoom(factor);
    };

    const resetCropper = () => {
      cropperBox.value.reset();
      croppedImg.value = '';
    };

    const loadImage = event => {
      const { files } = event.target;

      if (files?.[0]) {
        const blob = URL.createObjectURL(files[0]);
        const reader = new FileReader();

        reader.readAsArrayBuffer(files[0]);

        reader.addEventListener('load', () => {
          img.value = blob;
        });
      }

      croppedImg.value = '';
    };

    return {
      img,
      img2,
      CircleStencil,
      croppedImg,
      cropperBox,
      getCrop,
      loadImage,
      zoom,
      resetCropper,
    };
  },
};
</script>

<style></style>
