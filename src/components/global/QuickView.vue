<template>
  <div class="quick-view mt-16">
    <v-dialog v-model="dialog" max-width="900" max-height="500">
      <v-icon
        style="
          position: absolute;
          right: -14px;
          top: -14px;
          background-color: black;
          color: white;
          font-size: 18px;
          padding: 13px;
          z-index: 10;
        "
        @click="dialog = false"
        >mdi-close</v-icon
      >
      <v-card elevation="0" class="content_card">
        <v-container fluid class="bg-white pt-10 px-10">
          <v-row>
            <v-col cols="7">
              <img
                :src="tab ? tab : product.thumbnail"
                class="w-100"
                alt=""
                height="400"
                v-if="!loading"
              />
              <v-skeleton-loader
                v-if="loading"
                type="image, image, image"
              ></v-skeleton-loader>
              <v-tabs center-active height="250" v-model="tab" class="mt-10">
                <v-tab
                  v-for="(img, i) in product.images"
                  :key="i"
                  class="mx-10"
                  :value="img"
                >
                  <img :src="img" alt="" width="60" height="100" />
                </v-tab>
              </v-tabs>
            </v-col>
            <v-col cols="5" class="pt-0 pl-6">
              <v-skeleton-loader
                v-if="loading"
                type="article, article, article"
              ></v-skeleton-loader>
              <v-card elevation="0" v-if="!loading">
                <v-card-title
                  class="px-0"
                  style="font-size: 19px; font-weight: bold"
                  >{{ product.title }} Sample - {{ product.category }} For
                  Sale</v-card-title
                >
                <div
                  class="rating-parent d-flex align-center"
                  style="gap: 10px"
                >
                  <v-rating
                    v-model="product.rating"
                    half-icreaments
                    readonly
                    color="yellow-darken-2"
                    size="x-small"
                    density="cobact"
                  ></v-rating>
                  <span
                    class="mt-1"
                    style="font-size: 13px; color: rgb(96, 96, 96)"
                    >Stock: {{ product.stock }}</span
                  >
                </div>
                <v-card-text
                  class="px-0"
                  style="font-size: 13px; color: rgb(96, 96, 96)"
                  >{{ product.description }}</v-card-text
                >
              </v-card>
              <v-card-text
                class="px-0 pt-0"
                style="font-size: 13px; color: rgb(96, 96, 96)"
                >Brand: {{ product.brand }}</v-card-text
              >
              <v-card-text
                class="px-0 pt-0"
                style="font-size: 13px; color: rgb(96, 96, 96)"
                >Availabilty:
                {{
                  product.stock > 0 ? "In Stock" : "Out Of Stock"
                }}</v-card-text
              >
              <v-card-text class="pl-1 pt-0">
                <del>${{ product.price }}</del> From
                <span
                  class="text-red"
                  style="font-weight: 900; font-size: 16px"
                >
                  ${{
                    Math.ceil(
                      product.price -
                        product.price * (product.discountPercentage / 100)
                    )
                  }}
                </span>
              </v-card-text>
              <v-card-text class="pl-0 ot-0"> Quantity</v-card-text>
              <div
                class="counter px-1"
                style="
                  border: 1px solid rgb(201, 201, 201);
                  border-radius: 30px;
                  width: fit-content;
                "
              >
                <v-icon size="22" @click="quantity > 1 ? quantity-- : false"
                  >mdi-minus</v-icon
                >
                <input
                  type="number"
                  style="
                    border: none;
                    outline: none;
                    width: 60px;
                    font-size: 15px;
                  "
                  class="text-center py-2"
                  min="1"
                  v-model="quantity"
                />
                <v-icon size="22" @click="quantity++">mdi-plus</v-icon>
              </div>
              <v-card-text class="pl-0">
                Subtotal: ${{
                  Math.ceil(
                    product.price -
                      product.price * (product.discountPercentage / 100)
                  ) * quantity
                }}
              </v-card-text>
              <v-card-actions class="mt-2 w-100 px-0">
                <v-btn
                  variant="outlined"
                  class="w-75 text-white"
                  density="compact"
                  height="50"
                  style="
                    text-transform: none;
                    border-radius: 30px;
                    background-color: red;
                  "
                  @click="addToCart(product)"
                  :loading="btnLoading"
                  >Add To Cart</v-btn
                >
              </v-card-actions>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import { VSkeletonLoader } from "vuetify/lib/components/index.mjs";
import { cartStore } from "@/stores/cart";
import { mapActions } from "pinia";
export default {
  inject: ["Emitter"],
  components: {
    VSkeletonLoader,
  },
  methods: {
    ...mapActions(cartStore, ["addItem"]),
    addToCart(item) {
      item.quantity = this.quantity;
      this.btnLoading = true;
      setTimeout(() => {
        this.btnLoading = false;
        this.addItem(item);
        this.Emitter.emit("openCart");
        this.Emitter.emit("showMsg", item.title);
        this.dialog = false;
      }, 1000);
    },
  },
  data: () => ({
    loading: false,
    tab: "",
    quantity: 1,
    dialog: false,
    product: "",
    btnLoading: false,
  }),
  mounted() {
    this.Emitter.on("openQuickView", (data) => {
      this.loading = true;
      this.product = data;
      this.dialog = true;
      setTimeout(() => {
        this.loading = false;
      }, 1000);
    });
  },
};
</script>

<style lang="scss">
.content_card {
  &::-webkit-scrollbar {
    width: 5px;
  }
  &::-webkit-scrollbar-thumb {
    width: 5px;
    background-color: rgb(209, 28, 28);
  }
  &::-webkit-scrollbar-track {
    width: 5px;
    background-color: rgb(163, 159, 159);
  }
}
</style>
