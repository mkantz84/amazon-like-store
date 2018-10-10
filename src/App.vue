<template>
  <div>
    <app-side-bar></app-side-bar>
    <app-header></app-header>
    <app-products></app-products>
  </div>
</template>

<script>
import SideBar from "./components/sideBar/SideBar";
import Header from "./components/Header";
import Products from "./components/products/Products";
import { eventBus } from './main.js';

export default {

  components: {
    appSideBar: SideBar,
    appHeader: Header,
    appProducts: Products
  },

  mounted() {
    eventBus.$emit('initProducts');
  }
}
</script>

<style>
  body {
    font-family: sans-serif;
    background-color: #e7e5e6;
  }

  button {
    background: unset;
    border: unset;
    color: white;
    cursor: pointer;
  }

  .slider-handle {
    background-color: #ff7a72;
    color: #ff7a72;
    background-image: unset;
  }

  .tooltip {
    display: none;
  }

  .slider.slider-horizontal {
    width: 60%;
  }

  .d-inline-block {
    padding: 0.5em 0 0.5em 4%;
  }
</style>
