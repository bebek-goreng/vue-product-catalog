<template>
  <div id="app">
    <div class="background" :style="{ backgroundColor: backgroundColor }"></div>
    <ProductCard>
      <ProductView @categoryChanged="updateCategory" />
    </ProductCard>
  </div>
</template>

<script>
import ProductCard from './components/Card.vue';
import ProductView from './views/Product.vue';

export default {
  name: 'App',
  components: {
    ProductCard,
    ProductView,
  },
  data() {
    return {
      currentCategory: ''
    };
  },
  computed: {
    backgroundColor() {
      if (this.currentCategory === "men's clothing") {
        return "#D6E6FF";
      } else if (this.currentCategory === "women's clothing") {
        return "#FDE2FF";
      } else {
        return "#DCDCDC"
      }
    }
  },
  methods: {
    updateCategory(category) {
      this.currentCategory = category;
    }
  }
}
</script>

<style>
body,
html {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

#app {
  width: 100vw;
  height: 100vh;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 70vh;
  background-image: url('@/assets/images/bg.png');
  background-size: cover;
  background-position: center;
  z-index: -1;
}
</style>
