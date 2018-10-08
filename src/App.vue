<template>
  <div>
    <app-side-bar></app-side-bar>
    <app-header></app-header>
    <app-products></app-products>
  </div>
</template>

<script>
import SideBar from "./components/SideBar";
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
</style>
