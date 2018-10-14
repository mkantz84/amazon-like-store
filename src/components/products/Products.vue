<template>
  <div class="products">
    <div class="pad">
      <app-product
        v-for="product in products.slice(0, 8 * iterations)"
        :key="product.id"
        :product="product"
        @showOpac="showOpacity = $event"></app-product>
      <br><br>
      <!-- each time we click this button, we adding 1 to the iteration,
      thus showing more products from the products array: -->
      <button
        class="more"
        @click="iterations++"
        v-if="products.length > 8 * iterations">
        MORE
        <img src="../../assets/more.png">
      </button>
    </div>
    <!-- this div will cover with an opacity all the products div -->
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
      // get all the products from data.js
      this.products = productsData;
    },

    factoryFilterSearch(filter, options) {
      switch (filter) {
        case "byName":
          this.filterByName(options.name);
          break;
        case "deals":
          this.sortDeals();
          break;
        case "refinSearch":
          this.refinSearch(options);
          break;
        default:
          break;
      }
    },

    filterByName(val) {
      this.iterations = 1;
      this.showOpacity = false;
      if (!val) {
        this.initProducts();
      } else {
        this.products = productsData.filter(
          elm => elm.title.toLowerCase().indexOf(val.toLowerCase()) > -1
        );
      }
      return this;  //support chaining
    },
    sortDeals() {
      this.products.sort(
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
    },
    filterByCondition(condition) {
      if(condition){
        this.products = this.products.filter(
          elm => elm.condition.toLowerCase() === condition
        );
      }
      return this;  //support chaining
    },
    filterByShipping(isFreeShipping) {
      if (isFreeShipping) {
        this.products = this.products.filter(
          elm => !elm.shippingCost
        );
      }
      return this;  //support chaining
    },
    filterByPriceRange(priceRange) {
      this.products = this.products.filter(
        elm => elm.price >= priceRange[0] && elm.price <= priceRange[1]
      );
      return this;  //support chaining
    },

    refinSearch(options) {
      this.filterByName(options.name)
        .filterByCondition(options.condition)
          .filterByShipping(options.shipping)
            .filterByPriceRange(options.priceRange);
    }
  },

  created() {
    var that = this;
    const options = {};
    eventBus.$on("initProducts", () => {
      this.initProducts();
    });
    eventBus.$on("searchName", name => {
      options.name = name;
      that.factoryFilterSearch("byName", options);
    });
    eventBus.$on("searchDeals", () => {
      that.factoryFilterSearch("deals");
    });
    eventBus.$on("refinSearch", options => {
      that.factoryFilterSearch("refinSearch", options);
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

