<template>
  <div class="alert">
    {{ text }}
  </div>
</template>

<script setup>
const props = defineProps(["text"]);
const text = props.text;
</script>

<style lang="scss"></style>
