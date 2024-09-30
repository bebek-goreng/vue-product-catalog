<template>
    <div class="container">
        <LoadingSpinner :isLoading="isLoading" />
        <div v-if="!isLoading && isValidCategory(product.category)" class="product-view">
            <div class="image-container">
                <img :src="product.image" alt="Product Image" />
            </div>
            <div class="content-container">
                <div>
                    <h1>{{ product.title }}</h1>
                    <div class="category">
                        <p class="category-text">{{ product.category }}</p>
                        <RatingProduct :rating="product.rating.rate" :ratingColor="getRatingColor(product.category)" />
                    </div>
                    <hr />
                </div>
                <div class="description">
                    <p>{{ product.description }}</p>
                </div>
                <div>
                    <hr />
                    <h2 :style="{ color: getPriceColor(product.category) }">${{ product.price }}</h2>
                    <div>
                        <ProductButton :category="product.category" :nextProduct="fetchNextProduct" />
                    </div>
                </div>
            </div>
        </div>
        <UnavailableProduct v-else-if="!isLoading && !isValidCategory(product.category)" :handleClick="fetchNextProduct"
            buttonName="Next Product" />
    </div>
</template>

<script>
import LoadingSpinner from '../components/Spinner.vue';
import ProductButton from '../components/Button.vue';
import RatingProduct from '../components/Rating.vue';
import UnavailableProduct from './UnavailableProduct.vue';

export default {
    name: 'ProductView',
    components: {
        LoadingSpinner,
        ProductButton,
        RatingProduct,
        UnavailableProduct
    },
    data() {
        return {
            product: {},
            currentProductId: 1,
            isLoading: false,
        };
    },
    created() {
        this.fetchProduct(this.currentProductId);
    },
    methods: {
        async fetchProduct(productId) {
            this.isLoading = true;
            try {
                const response = await fetch(`https://fakestoreapi.com/products/${productId}`);
                const data = await response.json();
                this.product = data;
                this.$emit('categoryChanged', data.category);
            } catch (error) {
                console.error('Error fetching product:', error);
            } finally {
                this.isLoading = false;
            }
        },
        fetchNextProduct() {
            this.currentProductId = this.currentProductId < 20 ? this.currentProductId + 1 : 1;
            this.fetchProduct(this.currentProductId);
        },
        getRatingColor(category) {
            return category === "men's clothing" ? '#002772' : category === "women's clothing" ? '#720060' : '#002772';
        },
        getPriceColor(category) {
            return category === "men's clothing" ? '#002772' : category === "women's clothing" ? '#720060' : '#002772';
        },
        isValidCategory(category) {
            return category === "men's clothing" || category === "women's clothing";
        }
    }
};
</script>

<style scoped src="@/assets/styles/ProductView.css"></style>
