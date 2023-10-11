<template>
    <v-card-item>
        <v-card-title>COS30043 - Interface Design and Development Restaurant</v-card-title>
        <v-card-subtitle>We take pride in our specialized Vietnamese cuisines!</v-card-subtitle>
    </v-card-item>
    <v-card-item class="m-2 p-3 elevation-4">
        <v-card-title>Dishes of the day</v-card-title>
        <v-row justify="center">
            <v-col v-for="food in randomFoods" :key="food.id" cols="12" sm="4">
                <v-img class="m-3" :src="food.image" :alt="food.name"></v-img>
            </v-col>
        </v-row>
    </v-card-item>
    <div v-if="loading">Loading reviews...</div>
    <div v-else>
        <v-sheet>
            <v-card-item>
                <v-card-title>Reviews from our valued customers</v-card-title>
                <v-card v-for="(review, index) in displayedReviews" :key="index" class="m-4 h-50">
                    <v-rating v-model="review.rating" empty-icon="mdi-heart-outline" full-icon="mdi-heart" color="#74C69D"
                        readonly></v-rating>
                    <v-card-text>{{ review.description }}</v-card-text>
                </v-card>
                <v-pagination v-model="currentPage" :length="Math.ceil(reviews.length / reviewsPerPage)"
                    @input="paginateReviews"></v-pagination>
            </v-card-item>
        </v-sheet>
    </div>
</template>
  
<script>
import axios from 'axios';
import 'bootstrap/dist/css/bootstrap.css';

export default {
    name: 'HomeComponent',
    data() {
        return {
            randomFoods: [],
            loading: true,
            reviews: [],
            currentPage: 1, // Current page of reviews
            reviewsPerPage: 5, // Number of reviews per page
        };
    },
    computed: {
        displayedReviews() {
            // Calculate the index range for the current page
            const startIndex = (this.currentPage - 1) * this.reviewsPerPage;
            const endIndex = startIndex + this.reviewsPerPage;

            // Slice the reviews array based on the index range
            return this.reviews.slice(startIndex, endIndex);
        },
    },
    mounted() {
        this.randomFoods = require('@/assets/food.json');
        this.generateRandomFoods();
        this.loadReviews();
    },
    methods: {
        loadReviews() {
            axios
                .get('https://mercury.swin.edu.au/cos30043/s103533680/api/api_review/apis_review.php')
                .then(response => {
                    this.reviews = response.data;
                    this.reviews.reverse();
                    this.loading = false;
                })
                .catch(error => {
                    console.error('Failed to load reviews:', error);
                    this.loading = false;
                });
        },
        paginateReviews(page) {
            this.currentPage = page;
        },
        generateRandomFoods() {
            const randomIndices = [];
            while (randomIndices.length < 3) {
                const randomIndex = Math.floor(Math.random() * this.randomFoods.length);
                if (!randomIndices.includes(randomIndex)) {
                    randomIndices.push(randomIndex);
                }
            }
            this.randomFoods = randomIndices.map(index => this.randomFoods[index]);
        }
    },
};
</script>
  