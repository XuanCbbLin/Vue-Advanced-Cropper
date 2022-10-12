<template>
  <div class="flex mb-4 items-center justify-center">
    <i-material-symbols-zoom-out-rounded />
    <input
      type="range"
      min="0"
      max="100"
      class="h-8 w-80"
      :value="slideValue"
      @input="$emit('update:slideValue', $event.target.value)"
    />
    <i-material-symbols-zoom-in-rounded />
  </div>
</template>

<script>
export default {
  props: {
    slideValue: Number,
  },
  setup() {},
};
</script>

<style lang="scss" scoped></style>
