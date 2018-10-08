<template>
  <div
    class="mainProduct"
    @mouseover="manageProductEye(true)"
    @mouseout="manageProductEye(false)"
    @click="showDetails"
    :class="{ mainProductBig: showMoreDetails }">
    <span class="title" :title="product.title">{{ product.title | maxLength(showMoreDetails) }}</span>
    <img class="productImage" :src="product.image" alt="product image">
    <div v-if="showMoreDetails">
      <div class="more">
        <span class="price" v-html="currency"></span>
      </div>
      <a
        :href="product.link"
        @click.stop=""
        target="_blank"
        class="getIt">
        GET IT
        <img src="../../assets/gettIt.png">
      </a>
    </div>
    <img
      class="productEye"
      v-if="showProductEye"
      src="../../assets/productHover.png">
  </div>
</template>

<script>
export default {
  props: ["product"],

  data() {
    return {
      showMoreDetails: false,
      showProductEye: false,
      currency: this.showCurrency()
    };
  },

  methods: {
    manageProductEye(show) {
      this.showProductEye = false;
      if (!this.showMoreDetails) {
        this.showProductEye = show;
      }
    },
    showCurrency() {
      const ammountArr = this.product.price.toString().split(".");
      let price =
        "$<span style='font-size: 1.5em;'>" + ammountArr[0] + "</span>";
      if (ammountArr[1]) {
        price += "." + ammountArr[1];
      }
      return price;
    },
    purchased() {
      alert('PURCHASED!');
    },
    showDetails() {
      this.showMoreDetails = !this.showMoreDetails;
      this.$emit('showOpac', this.showMoreDetails);
    }
  },

  watch: {
    showMoreDetails(val) {
      if(val) {
        this.showProductEye = false;
      }
    }
  },

  filters: {
    maxLength(value, showMoreDetails) {
      if (value.length > 30 && !showMoreDetails) {
        return (value.substring(0, 30) + "...").toUpperCase();
      }
      return value.toUpperCase();
    }
  }
};
</script>

<style scoped>
.mainProduct {
  display: inline-flex;
  width: 11em;
  height: 11em;
  background-color: white;
  margin: 1em;
  position: relative;
  border-radius: 0.3em;
  box-shadow: rgba(171, 171, 171, 0.7) 0px 0px 15px 2px;
  cursor: pointer;
  transition: 0.5s;
}

.productImage {
  max-height: 70%;
  max-width: 100%;
  margin: auto;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
}

.title {
  margin: 0.5em;
  display: inline-block;
}

span {
  color: #1a485e;
  font-size: 0.8em;
}

.productEye {
  position: absolute;
  bottom: 5%;
  right: 5%;
  height: 15%;
}

.mainProductBig {
  width: 24em;
  transition: 0.5s;
  z-index: 6001
}

.mainProductBig .title {
  max-width: 50%;
}

.mainProductBig .productImage {
  top: 0;
  bottom: initial;
  left: initial;
  right: 2%;
  max-width: 47%;
}

.more {
  position: absolute;
  bottom: 5%;
  left: 0;
}

.price {
  margin-left: 1em;
  font-weight: bold;
}

.getIt {
  position: absolute;
  bottom: 0.2em;
  right: 1em;
  float: right;
  background-color: #f6796f;
  color: white;
  padding: 0 0.7em;
  line-height: 2em;
  /* cursor: pointer; */
  text-decoration: none;
}

.getIt img {
  height: 1.3em;
  vertical-align: middle;
  margin-left: 0.5em;
}
</style>

