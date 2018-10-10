<template>
  <div class="sideBar">
    <img src="../../assets/stuff.png" alt="logo">
    <div class="options">
      <input
        type="text"
        placeholder="SEARCH FOR..."
        v-model.lazy="searchFor"><br>
      <button>CATEGORIES</button><br>
      <button @click="searchDeals">HOTTEST DEALS</button><br>
    </div>
    <div>
      <div
        @click="showMoreFilters = !showMoreFilters"
        class="refine"
        :class="{showRefineDiv: showMoreFilters}">
        <button>REFINE SEARCH</button>
      </div>
      <transition name="fade">
        <app-refine-search
          v-if="showMoreFilters"
          :name="searchFor">
        </app-refine-search>
      </transition>

    </div>
  </div>
</template>

<script>
import { eventBus } from "../../main.js";
import RefineSearch from "./RefineSearch";

export default {
  data() {
    return {
      searchFor: "",
      showMoreFilters: false,
    };
  },

  watch: {
    searchFor(value) {
      eventBus.$emit("searchName", value.trim());
    }
  },

  methods: {
    searchDeals() {
      eventBus.$emit("searchDeals");
    }
  },

  components: {
    appRefineSearch: RefineSearch
  }
};
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
  margin: 0 0 9% 15%;
}

input[type="text"] {
  padding: 0.5em;
  padding-left: 1em;
  border: transparent;
  border-radius: 0.3em;
  background-image: url("../../assets/input-logo.png");
  background-repeat: no-repeat;
  background-position: right;
  background-size: 2em;
}

.options button {
  display: inline-block;
  margin-top: 2.5em;
  color: white;
  cursor: pointer;
}

.refine {
  color: white;
  padding: 5%;
  padding-left: 16%;
  display: block;
  cursor: pointer;
}

.refine:hover,
.showRefineDiv {
  background: url('../../assets/refine.png') no-repeat top left #3e6074;
  background-size: contain;
  background-position: 18%;
  padding-left: 26%;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;

  /*option for slider:
  overflow-y: hidden;
	max-height: 500px;
	transition-property: all;
	transition-duration: .5s; */
}
.fade-enter, .fade-leave-to {
  opacity: 0;

  /*option for slider:
   max-height: 0; */
}
</style>


