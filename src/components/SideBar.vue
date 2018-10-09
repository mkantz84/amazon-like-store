<template>
  <div class="sideBar">
    <img src="../assets/stuff.png" alt="logo">
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

      <div class="refineDiv" v-if="showMoreFilters">
        <div class="priceRange">
          <strong>PRICE</strong>
          <b-form-slider
            v-model="rangeValue"
            range :min="0" :max="1500"
            @change="change">
          </b-form-slider>
          <span>{{ rangeValue[0] }}</span>
          <span style="float: right;margin-right: 32%;">{{ rangeValue[1] }}</span>
          <button>GO</button>
        </div>

        <div class="condition">
          <strong>CONDITION</strong>
          <label for="new">
            <input
              type="radio"
              id="new"
              value="new"
              v-model="condition"> New
          </label>
          <label for="used">
            <input
              type="radio"
              id="used"
              value="used"
              v-model="condition"> Used
          </label>
          <label for="refurbished">
            <input
              type="radio"
              id="refurbished"
              value="refurbished"
              v-model="condition"> Refurbished
          </label>
        </div>

        <label for="shipping">
            <input
              type="checkbox"
              id="shipping"
              value="shipping"
              v-model="shipping"> FREE SHIPPING
          </label>
      </div>


    </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
import { bFormSlider } from "vue-bootstrap-slider";
import "bootstrap-slider/dist/css/bootstrap-slider.css";

export default {
  data() {
    return {
      searchFor: "",
      basicValue: 50,
      rangeValue: [0, 1500],
      showMoreFilters: false,
      condition: "",
      shipping: false
    };
  },

  watch: {
    searchFor(value) {
      eventBus.$emit("refineSearch", value.trim());
    }
  },

  methods: {
    searchDeals() {
      eventBus.$emit("searchDeals");
    },
    change(value) {
      console.log(value);
    }
  },

  components: {
    bFormSlider
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
  background-image: url("../assets/input-logo.png");
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
  background: url(/dist/refine.png?fd815ed…) no-repeat top left #3e6074;
  background-size: contain;
  background-position: 18%;
  padding-left: 26%;
}

.refineDiv {
  background-color: #3e6074;
  padding: 0.5em 0 1em 18%;
  color: white;
  font-size: 0.8em;
}

.condition {
  padding-right: 20%;
}

.condition strong {
  display: block;
  padding: 1em 0 0.5em 0;
}

.condition label {
  margin-right: 22%;
}

.condition input {
  margin-left: 0;
}

input[type="checkbox"]{
  margin: 2em 3px 3px 0;
}

.priceRange {
  position: relative;
}

.priceRange button {
  position: absolute;
  right: 7%;
  top: 30%;
  background-color: #1a485e;
  height: 2em;
  width: 3em;
  border-radius: 0.3em;
}
</style>


