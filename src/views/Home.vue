<template>
  <div class="wrapper">
    <h1>SPACER</h1>
    <div class="search">
      <label for="search">Search</label>
      <input
        id="search"
        type="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
      <ul>
        <li v-for="item in resoults" :key="item.data[0].nasa_id">
          <p>{{ item.data[0].description }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'Home',
  data() {
    return {
      searchValue: '',
      resoults: [],
    };
  },
  methods: {
    // eslint-disable-next-line func-names
    handleInput: debounce(function () {
      console.log(this.searchValue);
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          console.log(response);
          this.resoults = response.data.collection.items;
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
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
}

.search {
  display: flex;
  flex-direction: column;
  width: 300px;

  input {
    height: 30px;
    border: 0;
    border-bottom: 1px solid black;
    outline: none;
  }
}

</style>
