<template>
    <div class="rating-container">
        <span class="rating-value">{{ rating }}/5</span>
        <div class="stars-container">
            <div v-for="star in 5" :key="star" class="star"
                :style="{ backgroundColor: star <= rating ? ratingColor : '#e0e0e0' }"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: "RatingProduct",
    props: {
        rating: {
            type: Number,
            required: true
        },
        ratingColor: {
            type: String,
            default: '#002772'
        }
    }
}
</script>

<style scoped src="@/assets/styles/Rating.css"></style>