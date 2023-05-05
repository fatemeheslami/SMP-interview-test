<template>
  <div>
    <v-row>
      <v-col cols="6">
        <h1>
          <strong>{{ product?.name }}</strong>
        </h1>
        <div class="d-flex justify-space-between">
          <div>
            <span class="">{{
              `${product?.relativeTime} در ${product?.city?.stateName}-${product?.city?.name} | ${product?.categoryName}`
            }}</span>
          </div>
          <div class="d-flex">
            <div class="action-btn">
              <span>
                4
                <v-icon>mdi-eye</v-icon>
              </span>
            </div>
            <div class="action-btn">
              <v-icon>mdi-share-variant-outline</v-icon>
            </div>
            <div>
              <v-icon>mdi-heart-outline</v-icon>
            </div>
          </div>
        </div>
        <div class="mt-5">
          <v-btn color="primary" size="small" class="ml-3">ارسال پیام</v-btn>
          <v-btn color="primary" size="small">اطلاعات تماس</v-btn>
        </div>
        <div class="mt-5">
          <div class="d-flex justify-center mt-4">
            <template v-for="headerItem in headerItems">
              <div
                :class="[
                  headerItem?.propertyTitle !== 'قیمت' ? 'action-btn' : '',
                ]"
                class="px-3"
              >
                <p class="text-center gray--text">
                  {{ headerItem?.propertyTitle }}
                </p>
                <p class="text-center">
                  {{ headerItem?.value }}
                  <span v-if="headerItem?.propertyTitle === 'قیمت'">{{
                    headerItem?.measurementUnitDisplayText
                  }}</span>
                </p>
              </div>
            </template>
          </div>
          <template v-for="item in items">
            <div class="d-flex justify-space-between mt-3">
              <p class="gray--text">{{ item?.propertyTitle }}</p>
              <p>{{ item?.value }}</p>
            </div>
            <v-divider />
          </template>
          <div class="mt-3">
            <strong>توضیحات</strong>
            <p class="mt-3">{{ product?.description }}</p>
          </div>
          <v-divider />
        </div>
      </v-col>
      <v-col cols="6">
        <v-window v-model="onboarding" show-arrows="hover">
          <v-window-item v-for="image in product.images" :key="image.fileId">
            <v-img :src="image?.fileUrl"></v-img>
          </v-window-item>
        </v-window>
        <div class="d-flex justify-center mt-5">
          <template v-for="image in product.images">
            <div>
              <v-img :src="image?.fileUrl" :width="100"></v-img>
            </div>
          </template>
        </div>
        <LeafletMap />
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      headerItems: [],
      items: [],
      onboarding: 0,
    };
  },
  components: {
    LeafletMap: () => import('./LeafletMap.vue')
  },
  mounted() {
    this.headerItems = this.product?.properties?.filter(
      (item) =>
        item.propertyTitle === "قیمت" ||
        item.propertyTitle === "برند" ||
        item.propertyTitle === "کشور سازنده"
    );
    this.items = this.product?.properties?.filter(
      (item) =>
        item.propertyTitle !== "قیمت" &&
        item.propertyTitle !== "برند" &&
        item.propertyTitle !== "کشور سازنده"
    );
  },
  props: {
    product: {
      type: Object,
      default: () => {},
    },
  },
};
</script>

<style scoped>
.action-btn {
  margin-left: 8px;
  padding-left: 8px;
  border-left: 1px solid #e2e8f0;
}
</style>
