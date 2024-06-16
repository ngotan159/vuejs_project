<template>
  <div class="home">
    <UpperBanner />
    <TheFeatures />
    <TopOffers />
    <ProductsSwiper
      :products="flashDeals"
      title="Flash Deals"
      titleColor="red"
    />
    <ToCats />
    <NewProducts :products="flashDeals" />
    <QualityFeatures />
    <ProductsSwiper :products="flashDeals" title="Products" titleColor="red" />
    <v-container fluid>
      <v-row>
        <v-col cols="6" class="pr-4">
          <img
            src="@/assets/images/band-left-cover.webp"
            alt=""
            class="w-100"
          />
        </v-col>
        <v-col cols="6" class="pl-4">
          <img
            src="@/assets/images/band-right-cover.webp"
            alt=""
            class="w-100"
          />
        </v-col>
      </v-row>
    </v-container>
    <ProductsSwiper :products="flashDeals" title="Products" titleColor="red" />
    <img src="@/assets/images/tv-banner.webp" class="w-100" alt="" />
    <ProductsSwiper :products="flashDeals" title="Products" titleColor="red" />
    <WhyShopwithus />
  </div>
</template>

<script>
import UpperBanner from "@/components/home_page/UpperBanner.vue";
import TheFeatures from "@/components/home_page/TheFeatures.vue";
import TopOffers from "@/components/home_page/TopOffers.vue";
import ProductsSwiper from "@/components/home_page/ProductsSwiper.vue";
import ToCats from "@/components/home_page/TopCategories.vue";
import NewProducts from "@/components/home_page/NewProducts.vue";
import QualityFeatures from "@/components/home_page/QualityFeatures.vue";
import WhyShopwithus from "@/components/home_page/WhyShopwithus.vue";
import { productsModule } from "@/stores/products";
import { mapActions, mapState } from "pinia";

export default {
  name: "HomeView",
  components: {
    UpperBanner,
    TheFeatures,
    TopOffers,
    ProductsSwiper,
    ToCats,
    NewProducts,
    QualityFeatures,
    WhyShopwithus,
  },
  computed: {
    ...mapState(productsModule, ["flashDeals", "newProducts", "mobilePhones"]),
  },
  methods: {
    ...mapActions(productsModule, ["getProducts"]),
  },
  async mounted() {
    await this.getProducts();
    console.log(this.flashDeals);
    console.log(this.newProducts);
    console.log(this.mobilePhones);
  },
};
</script>
