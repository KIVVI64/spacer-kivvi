<template>
  <div class="heroimage"></div>
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style>
.heroimage {
  position: fixed;
  top: 0;
  z-index: -1;
  width: 100%;
  height: 100vh;
  background-image: url('../assets/background.jpg');
  background-size: cover;
  background-position: center center;
}
.heroimage:after {
  content: '';
  background: rgba(0, 0, 0, .3);
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
  height: 100vh;
}
</style>
