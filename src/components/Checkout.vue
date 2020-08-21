<template>
  <div>
    <div class="container-fluid">
      <div class="row">
        <div class="col-bg-dark text-white">
          <a href class="navbar-brand">SPORTS STORE</a>
        </div>
      </div>
    </div>
    <div class="form-group m-2">
      <label for>Name</label>
      <input type="text" v-model="$v.order.name.$model" class="form-control" />
      <validation-error :validation="$v.order.name" />
    </div>
    <div class="form-group m-2">
      <label for>Email</label>
      <input type="text" v-model="$v.order.email.$model" class="form-control" />
      <validation-error :validation="$v.order.email" />
    </div>
    <div class="form-group m-2">
      <label for>Address</label>
      <input type="text" v-model="$v.order.address.$model" class="form-control" />
      <validation-error :validation="$v.order.address" />
    </div>
    <div class="form-group m-2">
      <label for>City</label>
      <input type="text" v-model="$v.order.city.$model" class="form-control" />
      <validation-error :validation="$v.order.city" />
    </div>
    <div class="form-group m-2">
      <label for>Zip</label>
      <input type="text" v-model="$v.order.zip.$model" class="form-control" />
      <validation-error :validation="$v.order.zip" />
    </div>
    <div class="text-center">
      <router-link to="/cart" class="btn btn-secondary m-1">Back</router-link>
      <button class="btn btn-primary m-1" @click="submitOrder">Place Order</button>
    </div>
  </div>
</template>

<script>
import { required, email } from "vuelidate/lib/validators";
import ValidationError from "./ValidationError";
import { mapActions } from "vuex";

export default {
  components: {
    ValidationError,
  },
  data() {
    return {
      order: {
        name: null,
        email: null,
        address: null,
        city: null,
        zip: null,
      },
    };
  },
  validations: {
    order: {
      name: { required },
      email: { required, email },
      address: { required },
      city: { required },
      zip: { required },
    },
  },
  methods: {
    ...mapActions({
      storeOrder: "storeOrder",
      clearCart: "cart/clearCartData",
    }),
    async submitOrder() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        let order = await this.storeOrder(this.order);
        this.clearCart();
        this.$router.push(`/thanks/${order}`);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>