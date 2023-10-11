<template>
    <v-card-item>
        <v-card-title>Menu</v-card-title>
        <v-card-subtitle></v-card-subtitle>
    </v-card-item>
    <v-card-item class="my-2">
        <v-sheet>
            <div class="container mx-auto align-items-center">
                <div class="row">
                    <div class="col-lg-4 col-md-6 col-sm-12" v-for="item in foodItems" :key="item.id">
                        <v-card max-width="300" max-height="300" class="m-4 p-2 elevation-2 custom-card">
                            <v-img :src="item.image" :alt="item.title" class="card-image"></v-img>
                            <v-card-text class="text-center">{{ item.title }}</v-card-text>
                        </v-card>
                    </div>
                </div>
            </div>
        </v-sheet>
    </v-card-item>
</template>
<script>
import 'bootstrap/dist/css/bootstrap.css';

export default {
    name: 'ComponentOne',
    data() {
        return {
            foodItems: []
        }
    },
    mounted() {
        this.foodItems = require('@/assets/food.json');
    },
};
</script>

<style>
.custom-card {
    aspect-ratio: 1 / 1;
    /* Set a fixed aspect ratio (1:1) */
}

@media (min-width: 600px) {
    .row {
        display: flex;
        flex-wrap: wrap;
    }

    .col-md-4 {
        flex: 0 0 33.3333%;
        max-width: 33.3333%;
    }
}
</style>