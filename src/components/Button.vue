<template>
    <div class="button-container">
        <button :style="{ backgroundColor: leftButtonColor, color: leftButtonTextColor }" class="dynamic-button">
            Buy now
        </button>
        <button @click="handleNextProduct" :style="{
            backgroundColor: rightButtonColor,
            border: `2px solid ${rightButtonBorderColor}`,
            color: rightButtonTextColor
        }" class="dynamic-button">
            Next product
        </button>
    </div>
</template>

<script>
export default {
    name: 'ProductButton',
    props: {
        category: {
            type: String,
            required: true,
        },
        nextProduct: {  
            type: Function,
            required: true,
        },
    },
    computed: {
        leftButtonColor() {
            return this.category === "women's clothing" ? '#720060' : '#002772';
        },
        leftButtonTextColor() {
            return 'white';
        },
        rightButtonColor() {
            return 'white';
        },
        rightButtonBorderColor() {
            return this.category === "women's clothing" ? '#720060' : '#002772';
        },
        rightButtonTextColor() {
            return this.category === "women's clothing" ? '#720060' : '#002772';
        },
    },
    methods: {
        handleNextProduct() {
            this.nextProduct();
        },
    },
}
</script>

<style scoped src="@/assets/styles/Button.css"></style>
