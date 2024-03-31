<script setup>
import SkeletonProductPage from './skeleton/SkeletonProductPage.vue'
</script>
<script>
export default {
  data() {
    return {
      product: null,
      id: 1,
      isLoading: false,
      isAvailable: false,
    };
  },
  methods: {
    toggleLoad () {
      this.isLoading = !this.isLoading;
    },

    async fetchProduct () {
      try {
        const response = await fetch(`https://fakestoreapi.com/products/${this.id}`);
        const responseData = await response.json();
        return responseData;
      } catch (error) {
        alert(error.message);
      }
    },

    async loadProduct () {
      this.toggleLoad();

      const product = await this.fetchProduct();

      if (product?.category == "men's clothing" || product?.category == "women's clothing") {
        this.product = product;
        this.isAvailable = true;
      }
      else {
        this.product = {};
        this.isAvailable = false;
      }

      if (this.id < 20) {
        this.id++;
      }
      else {
        this.id = 1;
      }

      this.toggleLoad();
    },

    
  },
  mounted() {
    this.loadProduct();
  }
};
</script>

<template>
  <div class="container relative" :class="!isAvailable? 'bg-unavailable' : product?.category == 'men\'s clothing' ? 'bg-men' : 'bg-women'">
    <div v-if="isLoading" class="relative"><SkeletonProductPage /></div>
    <div v-if="!isAvailable" class="card flex-column sad-face">
      <div class="content-unavailable">
        <p>This product is unavailable to show</p>
        <button @click="loadProduct" class="border-men button">Next product</button>
      </div>
    </div>

    <span v-if="isAvailable" class="bg-pattern"></span>
    <div v-if="product && isAvailable" class="card">
      <div class="card-image">
        <img :src="product?.image">
      </div>
      <div class="product-desc">
        <div class="desc-section">
          <h2 class="">{{ product?.title }}</h2>
          <div class="flex gap-1">
            <div class="grow-1 product-category">{{ product?.category }}</div>
            <div>{{ product?.rating?.rate }}/5</div>
            <div class="product-rating">
              <span v-for="i in 3" :key="i">
                <div class="rounded-full-solid" :class="product?.category == 'men\'s clothing' ? 'bgc-men' : 'bgc-women'"></div>
              </span>
              <span v-for="i in 2" :key="i">
                <div class="rounded-full" :class="product?.category == 'men\'s clothing' ? 'border-men' : 'border-women'"></div>
              </span>
            </div>
          </div>
          <hr>
          <div class="description-text">{{ product?.description }}</div>
          <hr>
        </div>
        <div class="flex flex-column men">
          <h2>
            ${{ product?.price }}
          </h2>
          <div class="flex gap-2 men">
            <button class="grow-1 button" :class="product?.category == 'men\'s clothing' ? 'bgc-men' : 'bgc-women'">Buy now</button>
            <button @click="loadProduct" class="grow-1 button" :class="product?.category == 'men\'s clothing' ? 'border-men' : 'border-women'">Next product</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
