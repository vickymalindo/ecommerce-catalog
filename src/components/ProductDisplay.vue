<template>
  <div :class="[category === 'women' ? 'bg-purple' : 'bg-blue']"></div>
  <div class="loader" v-if="isLoading"></div>
  <div class="product" v-else>
    <div class="container">
      <img :src="product.image" alt="baju" class="img" />
      <div class="upper">
        <h3 :class="[category === 'women' ? 'title-women' : 'title-men']">
          {{ product?.title }}
        </h3>
        <div class="rating-category">
          <span class="category">{{ product?.category }}</span>
          <div class="rating">
            <div class="rate">{{ product?.rating?.rate }}/5</div>
            <div class="stars" v-if="product?.rating?.rate <= 1">
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
            </div>
            <div class="stars" v-else-if="product?.rating?.rate <= 2">
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
            </div>
            <div class="stars" v-else-if="product?.rating?.rate <= 3">
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
            </div>
            <div class="stars" v-else-if="product?.rating?.rate <= 4">
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'disabled-women' : 'disabled-men'
                "></div>
            </div>
            <div class="stars" v-else>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
              <div
                :class="
                  category === 'women' ? 'active-women' : 'active-men'
                "></div>
            </div>
          </div>
        </div>
        <hr />
        <p class="desc">
          {{ product?.description }}
        </p>
        <div class="bottom">
          <hr />
          <p :class="[category === 'women' ? 'price-women' : 'price-men']">
            ${{ product?.price }}
          </p>
          <div class="wrapper-btn">
            <button
              @click="buyProduct"
              :class="[category === 'women' ? 'buy-women' : 'buy-men']">
              Buy now
            </button>
            <button
              @click="nextProduct((id = id + 1))"
              :class="[category === 'women' ? 'next-women' : 'next-men']">
              Next product
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductDisplay',
  data() {
    return {
      product: {},
      id: 1,
      category: '',
      isLoading: true,
    };
  },
  methods: {
    async nextProduct(id) {
      console.log(id);
      if (id === 21) {
        this.id = 1;
      }
      this.isLoading = true;
      const res = await fetch(`https://fakestoreapi.com/products/${this.id}`);
      const data = await res.json();
      console.log(data);
      const men = /women/g;
      const category = data.category;
      const background = category.match(men);
      console.log(background);
      const [gender] = background ?? ['men'];
      if (gender === 'women') {
        this.category = 'women';
      } else {
        this.category = 'men';
      }
      this.isLoading = false;
      this.product = data;
    },
    buyProduct() {
      alert('Untuk sementara fitur sedang dikembangkan');
    },
  },
  mounted() {
    this.nextProduct();
  },
};
</script>
