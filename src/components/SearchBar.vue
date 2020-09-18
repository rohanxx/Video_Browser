<template>
  <div class="search-container">
    <input class="form-control" @input="onInput" placeholder="Type something" />
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  methods: {
    onInput: function(event) {
      this.$emit("termChange", event.target.value);
    }
  }
};
</script>

<style>
.search-container {
  width: 60%;
  margin: 2rem auto;
}
</style>
