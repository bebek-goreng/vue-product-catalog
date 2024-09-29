<template>
    <div class="unavailable-product-container">
        <p>This product is unavailable to show</p>
        <button @click="handleClick">{{ buttonName }}</button>
    </div>
</template>

<script>
export default {
    name: "UnavailableProduct",
    props: {
        handleClick: {
            type: Function,
            required: true,
        },
        buttonName: {
            type: String,
            required: true,
        },
    },
};
</script>

<style scoped src="../assets/styles/UnavailableProduct.css"></style>