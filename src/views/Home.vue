<template>
  <div :class="[ { flexStart: step === 1} , 'wrapper']">
    <transition name="slide">
      <img src="../assets/logo.png" alt="Logo" class="logo" v-if="step === 1">
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0" />
    <Search v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="resoults" v-if="resoults && !loading && step === 1">
      <Item
        v-for="item in resoults"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import Search from '@/components/Search.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'Home',
  components: {
    Claim,
    Search,
    HeroImage,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      resoults: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    // eslint-disable-next-line func-names
    handleInput: debounce(function () {
      console.log(`Wyszukiwanie: ${this.searchValue}`);
      this.loading = true;
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          console.log(response);
          this.resoults = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 900),
  },
};
</script>

<style lang="scss" scoped>

.wrapper {
  position: relative;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  /*padding: 30px;*/
  padding-top: 10px;
  width: 100%;

  &.flexStart {
    justify-content: flex-start;
  }
}

.logo {
  position: absolute;
  top: 10px;
  left: 17px;
  height: 50px;
  width: auto;
}

.resoults {
  margin: 60px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 20px;

  @media (max-width: 1300px) {
    grid-template-columns: 1fr 1fr 1fr;
  }
  @media (max-width: 980px) {
    grid-template-columns: 1fr 1fr;
  }
  @media (max-width: 660px) {
    grid-template-columns: 1fr;
  }
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: margin-top 1s ease;
}
.slide-enter, .slide-leave-to {
  margin-top: -60px;
}

</style>
