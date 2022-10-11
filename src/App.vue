<template>
  <div class="flex">
    <div>
      <cropper
        class="bg-light-100 h-[600px] mb-4 w-[600px]"
        ref="cropperBox"
        :src="img"
        :stencil-component="$options.components.CircleStencil"
      />
      <div class="ml-5">
        <button class="ml-3" @click="getCrop">裁切圖片</button>
        <button class="ml-3" @click="zoom(2)">放大</button>
        <button class="ml-3" @click="zoom(0.5)">縮小</button>
        <input class="ml-3" type="file" @change="loadImage($event)" accept="image/*" />
      </div>
    </div>
    <div class="rounded-full h-[300px] ml-8 w-[300px] overflow-hidden">
      <img :src="cropedImg" v-if="cropedImg" />
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import { Cropper, CircleStencil } from 'vue-advanced-cropper';
import 'vue-advanced-cropper/dist/style.css';
import img2 from '../public/berserk.jpeg';

export default {
  components: {
    Cropper,
    CircleStencil,
  },
  setup() {
    const img = ref(
      'https://images.unsplash.com/photo-1600984575359-310ae7b6bdf2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=700&q=80'
    );

    const cropperBox = ref(null);
    const cropedImg = ref('');

    const getCrop = () => {
      const { canvas } = cropperBox.value.getResult();

      cropedImg.value = canvas.toDataURL();
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
    };

    const zoom = factor => {
      cropperBox.value.zoom(factor);
    };

    return {
      img,
      img2,
      cropedImg,
      cropperBox,
      getCrop,
      loadImage,
      zoom,
    };
  },
};
</script>

<style scoped></style>
