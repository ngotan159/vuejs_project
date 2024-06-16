<template>
  <div class="product-details mt-16">
    <h1>Product Details</h1>
    <v-container fluid>
      <v-row>
        <v-col cols="7">
          <img
            :src="tab ? tab : signelProduct.thumbnail"
            class="w-100"
            alt=""
            height="500"
            v-if="!loading"
          />
          <v-skeleton-loader
            v-if="loading"
            type="image, image, image"
          ></v-skeleton-loader>
          <v-tabs center-active height="250" v-model="tab" class="mt-10">
            <v-tab
              v-for="(img, i) in signelProduct.images"
              :key="i"
              class="mx-10"
              :value="img"
            >
              <img :src="img" alt="" width="100" height="200" />
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
              >{{ signelProduct.title }} Sample -
              {{ signelProduct.category }} For Sale</v-card-title
            >
            <div class="rating-parent d-flex align-center" style="gap: 10px">
              <v-rating
                v-model="signelProduct.rating"
                half-icreaments
                readonly
                color="yellow-darken-2"
                size="x-small"
                density="cobact"
              ></v-rating>
              <span class="mt-1" style="font-size: 13px; color: rgb(96, 96, 96)"
                >Stock: {{ signelProduct.stock }}</span
              >
            </div>
            <v-card-text
              class="px-0"
              style="font-size: 13px; color: rgb(96, 96, 96)"
              >{{ signelProduct.description }}</v-card-text
            >
          </v-card>
          <v-card-text
            class="px-0 pt-0"
            style="font-size: 13px; color: rgb(96, 96, 96)"
            >Brand: {{ signelProduct.brand }}</v-card-text
          >
          <v-card-text
            class="px-0 pt-0"
            style="font-size: 13px; color: rgb(96, 96, 96)"
            >Availabilty:
            {{
              signelProduct.stock > 0 ? "In Stock" : "Out Of Stock"
            }}</v-card-text
          >
          <v-card-text class="pl-1 pt-0">
            <del>${{ signelProduct.price }}</del> From
            <span class="text-red" style="font-weight: 900; font-size: 16px">
              ${{
                Math.ceil(
                  signelProduct.price -
                    signelProduct.price *
                      (signelProduct.discountPercentage / 100)
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
              style="border: none; outline: none; width: 60px; font-size: 15px"
              class="text-center py-2"
              min="1"
              v-model="quantity"
            />
            <v-icon size="22" @click="quantity++">mdi-plus</v-icon>
          </div>
          <v-card-text class="pl-0">
            Subtotal: ${{
              Math.ceil(
                signelProduct.price -
                  signelProduct.price * (signelProduct.discountPercentage / 100)
              ) * quantity
            }}
          </v-card-text>
          <v-card-actions class="mt-7 w-100 px-0">
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
              @click="addToCart(signelProduct)"
              :loading="btnLoading"
              >Add To Cart</v-btn
            >
          </v-card-actions>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import { productsModule } from "@/stores/products";
import { mapActions, mapState } from "pinia";
import { VSkeletonLoader } from "vuetify/lib/components/index.mjs";
import { cartStore } from "@/stores/cart";
export default {
  inject: ["Emitter"],
  computed: {
    ...mapState(productsModule, ["signelProduct"]),
  },
  methods: {
    ...mapActions(productsModule, ["getSingleProduct"]),
    ...mapActions(cartStore, ["addItem"]),
    addToCart(item) {
      item.quantity = this.quantity;
      this.btnLoading = true;
      setTimeout(() => {
        this.btnLoading = false;
        this.addItem(item);
        this.Emitter.emit("openCart");
        this.Emitter.emit("showMsg", item.title);
      }, 1000);
    },
  },
  components: {
    VSkeletonLoader,
  },
  data: () => ({
    loading: false,
    tab: "",
    quantity: 1,
    btnLoading: false,
    product: {
      id: 2,
      title: "Eyeshadow Palette with Mirror",
      description:
        "The Eyeshadow Palette with Mirror offers a versatile range of eyeshadow shades for creating stunning eye looks. With a built-in mirror, it's convenient for on-the-go makeup application.",
      category: "beauty",
      price: 19.99,
      discountPercentage: 5.5,
      rating: 3.28,
      stock: 44,
      tags: ["beauty", "eyeshadow"],
      brand: "Glamour Beauty",
      sku: "MVCFH27F",
      weight: 3,
      dimensions: {
        width: 12.42,
        height: 8.63,
        depth: 29.13,
      },
      warrantyInformation: "1 year warranty",
      shippingInformation: "Ships in 2 weeks",
      availabilityStatus: "In Stock",
      reviews: [
        {
          rating: 4,
          comment: "Very satisfied!",
          date: "2024-05-23T08:56:21.618Z",
          reviewerName: "Liam Garcia",
          reviewerEmail: "liam.garcia@x.dummyjson.com",
        },
        {
          rating: 1,
          comment: "Very disappointed!",
          date: "2024-05-23T08:56:21.618Z",
          reviewerName: "Nora Russell",
          reviewerEmail: "nora.russell@x.dummyjson.com",
        },
        {
          rating: 5,
          comment: "Highly impressed!",
          date: "2024-05-23T08:56:21.618Z",
          reviewerName: "Elena Baker",
          reviewerEmail: "elena.baker@x.dummyjson.com",
        },
      ],
      returnPolicy: "30 days return policy",
      minimumOrderQuantity: 32,
      meta: {
        createdAt: "2024-05-23T08:56:21.618Z",
        updatedAt: "2024-05-23T08:56:21.618Z",
        barcode: "2817839095220",
        qrCode: "https://dummyjson.com/public/qr-code.png",
      },
      images: [
        "https://cdn.dummyjson.com/products/images/beauty/Eyeshadow%20Palette%20with%20Mirror/1.png",
      ],
      thumbnail:
        "https://cdn.dummyjson.com/products/images/beauty/Eyeshadow%20Palette%20with%20Mirror/thumbnail.png",
    },
  }),
  async beforeMount() {
    this.loading = true;
    await this.getSingleProduct(this.$route.params.productId);
    this.loading = false;
  },
};
</script>
