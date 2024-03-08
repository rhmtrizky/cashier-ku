<template>
  <v-row cols="12">
    <v-col>
      <h2>Order</h2>
      <v-list>
        <v-list-item v-for="(item, index) in cartItems" :key="index">
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
            <v-list-item-subtitle class="d-flex">
              {{ currency(item.price) }}
              <div class="ml-5">
                <v-btn x-small icon color="primary" @click="decrement(item.id)">
                  <v-icon>mdi-minus</v-icon>
                </v-btn>
                x{{ item.quantity }}
                <v-btn x-small icon color="primary" @click="increment(item.id)">
                  <v-icon>mdi-plus</v-icon>
                </v-btn>
              </div>
            </v-list-item-subtitle>
          </v-list-item-content>
          <v-list-item-action>
            <v-btn x-small icon color="error" @click="removeItem(item.id)">
              <v-icon>mdi-close-thick</v-icon>
            </v-btn>
            <v-list-item-subtitle>{{
              currency(itemTotal(item.price, item.quantity))
            }}</v-list-item-subtitle>
          </v-list-item-action>
        </v-list-item>
        <v-list-item
          v-if="items.length"
          class="text-h6 black--text grey lighten-2"
        >
          <v-list-item-content>
            <v-list-item-title>Sub Total</v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
            <v-list-item-title>{{ currency(subTotal) }}</v-list-item-title>
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </v-col>
  </v-row>
</template>

<script>
import { mapState, mapGetters, mapActions } from "vuex";
export default {
  methods: {
    ...mapActions("carts", {
      increment: "increment",
      decrement: "decrement",
      removeItem: "removeItem",
    }),
    currency(value) {
      return Intl.NumberFormat("id-ID", {
        style: "currency",
        currency: "IDR",
      }).format(value);
    },
  },
  computed: {
    ...mapState("carts", {
      items: "items",
    }),
    ...mapGetters("carts", {
      cartItems: "cartItems",
      itemTotal: "itemTotal",
      subTotal: "subTotal",
    }),
  },
};
</script>
