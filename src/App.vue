<template>
  <div class="container">
    <div class="row">
      <div class="col-md-7">
        <div class="row">
          <div :key="product.id" class="col-md-6" v-for="product in products">
            <product
              :isInCart="isInCart(product)"
              :product="product"
              v-on:add-to-cart="addToCart(product)"
            ></product>
          </div>
        </div>
      </div>
      <div class="col-md-5 my-5">
        <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"></cart>
      </div>
    </div>

    <img src="assets/logo.png" alt="Vue Logo">
  </div>
</template>

<script>
import products from "@/products.json";
import Product from "@/components/Products.vue";
import Cart from "@/components/Cart.vue";

export default {
  name: "app",
  components: {
    Product,
    Cart
  },
  data() {
    return {
      products,
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    isInCart(product) {
      const item = this.cart.find(item => item.id === product.id);

      if (item) {
        return true;
      } else {
        return false;
      }
    },
    removeFromCart(product) {
      this.cart = this.cart.filter(item => item.id != product.id);
    },
    pay() {
      this.cart = [];
      alert("Shopping Completed");
    }
  }
};
</script>

<style>
body {
  background-color: #fbf8f3;
}
</style>
