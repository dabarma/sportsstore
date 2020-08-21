<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col bg-dark text-white">
        <a href class="navbar-brand">SPORTS STORE</a>
        <cart-summary />
      </div>
    </div>
    <div class="row">
      <div class="col-3 bg-info p-2">
        <CategoryControls />
        <button class="btn btn-block btn-warning mt-5" @click="setShowSearch(true)">Search</button>
      </div>
      <div class="col-9 p-2">
        <Search />
        <ProductList />
      </div>
    </div>
  </div>
</template>

<script>
import ProductList from "@/components/ProductList.vue";
import CategoryControls from "@/components/CategoryControls.vue";
import CartSummary from "@/components/CartSummary.vue";
import Search from "@/components/Search.vue";
import { mapMutations } from "vuex";

export default {
  components: {
    ProductList,
    CategoryControls,
    CartSummary,
    Search,
  },
  methods: {
    ...mapMutations(["setShowSearch"]),
  },
};
</script>

<style lang="scss" scoped>
</style>