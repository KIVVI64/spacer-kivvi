<template>
  <div class="modal">
    <div class="outerWrapper">
      <div class="innerWrapper">
        <div class="photo">
          <img :src="photo" :alt="title">
        </div>
        <div class="description">
          <h2>{{ title }}</h2>
          <hr>
          <p>{{ description }}</p>
        </div>
        <div class="close" @click="$emit('closeModal')"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description;
  },
};
</script>

<style lang="scss" scoped>
.modal {
  background-color: rgba(0, 0, 0, 0.3);
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
}

.outerWrapper {
  background: #fafafa;
  max-width: 100%;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;

  @media (min-width: 1024px) {
    max-width: 70%;
    height: 60%;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
    box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
  }
}

.close {
  position: absolute;
  right: 0;
  top: 0;
  width: 30px;
  height: 30px;
  margin: 10px;

  &::before,
  &::after {
    position: absolute;
    content: '';
    top: 16px;
    right: 6px;
    width: 20px;
    height: 2px;
    background: black;
    display: block;
  }
  &::before {
    transform: rotate(45deg);
  }
  &::after {
    transform: rotate(-45deg);
  }
}

.innerWrapper {
  display: flex;
  height: 100%;
  padding: 30px;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  @media (min-width: 1024px) {
    flex-direction: row;
    .photo {
      max-width: 60%;
      min-width: 55%;
      margin-right: 20px;
    }
  }

  .photo {
    width: 100%;
    height: auto;

    img {
      width: 100%;
      min-width: 300px;
    }
  }
}
</style>
