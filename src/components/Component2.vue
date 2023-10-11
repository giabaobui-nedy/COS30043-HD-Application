<template>
    <v-card-item>
        <v-card-title>Review</v-card-title>
        <v-card-subtitle>Our motto is to improve the service every day. Therefore, we highly appreciate feedbacks from you
            experience.</v-card-subtitle>
    </v-card-item>
    <v-card-item class="my-4">
        <v-sheet max-width="500" class="m-2 mx-auto">
            <v-form class="border elevation-4 rounded-lg p-3">
                <div class="text-center">
                    <v-rating v-model="rating" empty-icon="mdi-heart-outline" full-icon="mdi-heart" color="#74C69D" hover
                        half-increments></v-rating>
                </div>
                <v-textarea v-model="description" label="Your review:" variant="outlined"></v-textarea>
                <v-alert v-if="sucMessage !== ''" color="#95D5B2" type="success" title="Appreciation!"
                    :text="sucMessage"></v-alert>
                <v-alert v-if="errMessage !== ''" color="#ffccd5" type="error" title="Please try again"
                    :text="errMessage"></v-alert>
                <v-btn @click="submitForm()" type="button" class="mt-2" text="Submit" block></v-btn>
            </v-form>
        </v-sheet>
    </v-card-item>
</template>
  
<script>
import '@mdi/font/css/materialdesignicons.css';
import 'bootstrap/dist/css/bootstrap.css';

export default {
    name: 'ComponentTwo',
    data() {
        return {
            rating: null,
            description: '',
            errMessage: '',
            sucMessage: ''
        };
    },
    methods: {
        validate() {
            if (this.rating === null) {
                this.errMessage += "Please give us a valid rating"
            }
            return this.rating !== null;
        },
        submitForm() {
            if (this.validate()) {
                const apiUrl = 'https://mercury.swin.edu.au/cos30043/s103533680/api/api_review/apis_review.php';
                fetch(apiUrl, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(this.review)
                })
                    .then(response => response.json())
                    .then(data => {
                        console.log('Data successfully posted:', data);
                        // Handle the response data as needed
                    })
                    .catch(error => {
                        console.error('Error posting data:', error);
                        // Handle the error
                    });
                this.sucMessage = "Thank you very much for your feedback. We are striving everyday to provide better services!"
                this.resetForm();
            }
        },
        resetForm() {
            this.rating = null;
            this.description = '';
            this.errMessage = '';
        }
    },
    computed: {
        review() {
            return {
                rating: this.rating,
                description: this.description
            }
        }
    }
};
</script>
  