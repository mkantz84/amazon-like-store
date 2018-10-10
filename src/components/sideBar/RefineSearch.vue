<template>
  <div class="refineDiv">
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
</template>

<script>
import { bFormSlider } from "vue-bootstrap-slider";
import "bootstrap-slider/dist/css/bootstrap-slider.css";
export default {
  data() {
    return {
      rangeValue: [0, 1500],
      condition: "",
      shipping: false
    };
  },

  components: {
    bFormSlider
  }
};
</script>

<style scoped>
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
  font-weight: bold;
}
</style>


