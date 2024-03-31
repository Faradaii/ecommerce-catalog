
<template>
  <div class="container-skeleton">
    <div class="card">
      <div class="card-image">
        <div class="image"></div>
      </div>
      <div class="product-desc">
        <div class="desc-section">
          <h2 class="product-title"> </h2>
          <div class="flex gap-1">
            <div class="grow-1 product-category"></div>
            <div class="product-rate"></div>
            <div class="product-rating">
              <span v-for="i in 5" :key="i">
                <div class="rounded-full-solid"></div>
              </span>
            </div>
          </div>
          <hr>
          <div class="description-text">
            <div class="grow-1 product-category"></div>
          </div>
          <hr>
        </div>
        <div class="flex flex-column men">
          <h2 class="product-price">
            
          </h2>
          <div class="flex gap-2 men no-skeleton">
            <button class="grow-1 button-skeleton"> </button>
            <button class="grow-1 button-skeleton"> </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>