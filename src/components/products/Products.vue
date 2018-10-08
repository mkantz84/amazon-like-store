<template>
  <div class="products">
    <div class="pad">
      <app-product
        v-for="product in products.slice(0, 8 * iterations)"
        :key="product.id"
        :product="product"
        @showOpac="showOpacity = $event"></app-product><br><br>
      <button
        class="more"
        @click="iterations++"
        v-if="products.length > 8 * iterations">
        MORE
        <img src="../../assets/more.png">
      </button>
    </div>
    <div v-if="showOpacity" class="opac"></div>
  </div>
</template>

<script>
import Product from "./Product";
import { eventBus } from "../../main.js";
import productsData from "../../data/data.js";

export default {
  data() {
    return {
      products: [],
      iterations: 1,
      showOpacity: false
    };
  },

  components: {
    appProduct: Product
  },

  methods: {
    initProducts() {
      this.products = productsData;
    }
  },

  created() {
    var that = this;
    eventBus.$on("initProducts", () => {
      this.initProducts();
    });
    eventBus.$on("refineSearch", val => {
      that.iterations = 1;
      that.showOpacity = false;
      if (!val) {
        that.initProducts();
      } else {
        that.products = that.products.filter(
          elm => elm.title.toLowerCase().indexOf(val.toLowerCase()) > -1
        );
      }
    });
    eventBus.$on("searchDeals", () => {
      that.products.sort(
        (a, b) =>
          a.listPrice > b.listPrice || a.listPrice === ""
            ? 1
            : b.listPrice > a.listPrice || b.listPrice === ""
              ? -1
              : a.price > b.price || a.price === ""
                ? 1
                : b.price > a.price || b.price === ""
                  ? -1
                  : 0
      );
    });
  }
};
</script>

<style scoped>
.products {
  width: 80%;
  height: 80%;
  position: fixed;
  right: 0;
  top: 20%;
  overflow: auto;
}

.pad {
  padding: 2em;
}

.more {
  background-color: #f6796f;
  color: white;
  padding: 0 0.5em;
  line-height: 2em;
  border-radius: 0.3em;
  width: 6.5em;
  margin: 0 auto;
  display: block;
}

.more img {
  height: 1.3em;
  vertical-align: middle;
  margin-left: 0.5em;
}

.opac {
  display: block;
  position: fixed;
  right: 0;
  top: 20%;
  width: 80%;
  height: 80%;
  background-color: black;
  opacity: 0.4;
  z-index: 6000;
}
</style>

