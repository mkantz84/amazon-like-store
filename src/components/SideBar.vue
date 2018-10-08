<template>
  <div class="sideBar">
    <img src="../assets/stuff.png" alt="logo">
    <div class="options">
      <input
        type="text"
        placeholder="SEARCH FOR..."
        v-model.lazy="searchFor"><br>
      <button>CATEGORIES</button><br>
      <button>HOTTEST DEALS</button><br>
      <button>REFINE SEARCH</button>
    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  data() {
    return {
      searchFor: ''
    }
  },

  watch: {
    searchFor(value) {
      eventBus.$emit('refineSearch', value);
    }
  }
}
</script>

<style scoped>
  .sideBar {
    height: 100%;
    width: 20%;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    background-color: #1a485e;
    overflow-x: hidden;
  }

  img {
    width: 100%;
  }

  .options {
    margin-left: 15%;
  }

  input[type=text] {
    padding: 0.5em;
    padding-left: 1em;
    border: transparent;
    border-radius: 0.3em;
    background-image: url('../assets/input-logo.png');
    background-repeat: no-repeat;
    background-position: right;
    background-size: 2em;
  }

  button {
    display: inline-block;
    margin-top: 2.5em;
    color: white;
    cursor: pointer;
  }
</style>


