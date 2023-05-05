<template>
  <div>
    <BreadCrumb :breadCrumb="breadCrumb"/>
    <ProductDetail :product="product" />
    <div class="mt-8">
      <div class="card">
          <h2 style="padding: 10px">آگهی های مشابه</h2>
          <v-row>
            <v-col cols="4">
              <AdvertiseCard :advertise="advertise"/>
            </v-col>
          </v-row>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  components: {
    ProductDetail: () => import("../components/ProductDetail.vue"),
    AdvertiseCard: () => import('../components/AdvertiseCard.vue'),
    BreadCrumb: () => import('../components/BreadCrumb.vue')
  },
  data() {
    return {
      product: {},
      breadCrumb: {},
      advertise: [],
    };
  },
  async fetch() {
    const [product, breadCrumb, advertise] = await Promise.all([
      this.$axios.$get("advertisements/331482168289153024"),
      this.$axios.$get("categories/266188222852255744/breadcrumb"),
      this.$axios.$get("advertisements/331482168289153024/related"),
    ]);
    this.product = product;
    this.breadCrumb = breadCrumb
    this.advertise = advertise;
  },
};
</script>

<style scoped>
.card {
  background-color: #fff;
  border: 1px solid rgba(0, 0, 0, 0.125);
  border-radius: 0.25rem;
  width: 100%;
}
</style>
