<template>
  <div :style="style" class="item">
  </div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.links[0].title,
    };
  },
  computed: {
    style() {
      return `background-image: url("${this.photo}")`;
    },
  },
};
</script>

<style>
.item {
  width: 300px;
  height: 400px;
  background-size: cover;
  background-position: center center;
}
</style>
