<template>
  <div class="searchwrapper">
    <label for="search">Search</label>
    <input
      id="search"
      name="search"
      :class="{ dark }"
      :value="value"
      @input="handleChange"
    />
  </div>
</template>

<script>
export default {
  name: 'Search',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.searchwrapper {
  display: flex;
  flex-direction: column;
  width: 300px;
  padding: 10px;
  color: #fafafa;

  label {
    display: none;
  }

  input {
    height: 30px;
    font-size: 20px;
    border: 0;
    background: none;
    border-bottom: 1px solid #fafafa;
    outline: none;
    color: #fafafa;
    text-align: center;
  }
  input:focus {
    border-bottom: 2px solid;
  }

  .dark {
    color: #212121;
    border-bottom-color: #212121;
  }
}
</style>
