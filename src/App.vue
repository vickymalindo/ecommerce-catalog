<template>
  <ProductDisplay />
  <!-- <h2>asdasds</h2> -->
</template>

<script>
import ProductDisplay from './components/ProductDisplay.vue';
export default {
  name: 'App',
  data() {
    return {
      isShow: true,
    };
  },

  components: {
    ProductDisplay,
  },
};
</script>
