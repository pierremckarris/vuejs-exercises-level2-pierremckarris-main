<template>
  <div>
    <h2>Add new order</h2>
    <form @submit.prevent="add">
      ...
      <button type="submit">Save</button>
      <router-link to="/"><button type="button">Cancel</button></router-link>
    </form>
    <p v-if="warning" class="warning">{{ warning }}</p>
  </div>
</template>

<script>
import { nanoid } from "nanoid"

export default {
  data() {
    return {
      order: {
        ...
      },
      warning: ""
    }
  },
  computed: {
    isFormValid() {
      return (
        this.order.sender &&
        this.order.destination &&
        this.order.weight > 0
      );
    }
  },
  methods: {
    add() {
      if (!this.isFormValid) {
        this.warning = "Please fill all the fields and ensure the weight is greater than 0 kg.";
        return;
      }
      
      this.order.id = this.newId();
      const storedOrders = JSON.parse(localStorage.getItem("orders")) || [];
      storedOrders.push(this.order);
      localStorage.setItem("orders", JSON.stringify(storedOrders));
      this.$router.push("/");
    },
    newId() {
      return nanoid();
    }
  }
}
</script>

<style>
.warning {
  color: yellow;
  font-weight: bold;
}
</style>
