<template>
    <v-card-title>Careers</v-card-title>
    <v-card-subtitle>Join our team at COS30043 - Interface Design and Development</v-card-subtitle>
    <v-card-text class="my-4">
        <v-sheet max-width="500" class="mx-auto">
            <v-form class="border elevation-4 rounded-lg p-3">
                <v-text-field v-model="name" label="Name"></v-text-field>
                <v-select v-model="appliedPosition" :items="positions" label="Applied Position"></v-select>
                <v-select v-model="appliedStore" :items="stores" label="Applied Store"></v-select>
                <v-text-field v-model="contactEmail" label="Contact Email"></v-text-field>
                <v-text-field v-model="contactPhone" label="Contact Phone"></v-text-field>
                <v-textarea v-model="personalDescription" label="Personal Description"></v-textarea>
                <v-file-input v-model="resumeFile" label="Your Resume"></v-file-input>
                <v-alert color="#95D5B2" v-if="sucMessage !== ''" type="success" title="Completed" :text="sucMessage"></v-alert>
                <v-alert color="#ffccd5" v-if="errMessage !== ''" type="error" title="Invalid inputs" :text="errMessage"></v-alert>
                <v-btn @click="submitForm" type="button" class="mt-2" text="Submit Application" block></v-btn>
                <v-btn @click="resetForm" type="reset" class="mt-2" text="Reset" block></v-btn>
            </v-form>
        </v-sheet>
    </v-card-text>
</template>
<script>
import 'bootstrap/dist/css/bootstrap.css';
export default {
    name: 'ComponentThree',
    data() {
        return {
            name: '',
            appliedPosition: '',
            appliedStore: '',
            positions: ['Casual Team Member', 'Part-Time Team Member', 'Full-Time Team Leader'],
            stores: [
                'VIC-CBD',
                'VIC-Carlton',
                'VIC-Fitzroy',
                'VIC-St Kilda',
                'VIC-Richmond',
                'VIC-Brunswick',
                'VIC-Southbank',
                'VIC-Collingwood',
                'VIC-Prahran',
                'VIC-South Yarra',
                'VIC-Toorak',
                'VIC-Footscray',
                'VIC-Camberwell',
                'VIC-Hawthorn',
                'VIC-Box Hill',
                'VIC-Doncaster'
            ],
            contactEmail: '',
            contactPhone: '',
            personalDescription: '',
            resumeFile: null,
            errMessage: '',
            sucMessage: ''
        };
    }, methods: {
        validateForm() {
            this.errMessage = ''; // Clear previous error messages

            if (!this.name) {
                this.errMessage += ' Name is required.';
            }

            if (!this.appliedPosition) {
                this.errMessage += ' Applied Position is required.';
            }

            if (!this.appliedStore) {
                this.errMessage += ' Applied Store is required.';
            }

            if (!this.contactEmail) {
                this.errMessage += ' Contact Email is required.';
            } else if (!/^[\w-]+(\.[\w-]+)*@([\w-]+\.)+[a-zA-Z]{2,7}$/.test(this.contactEmail)) {
                this.errMessage += ' Invalid Contact Email.';
            }

            if (!this.contactPhone) {
                this.errMessage += ' Contact Phone is required.';
            } else if (!/^\d{10}$/.test(this.contactPhone)) {
                this.errMessage += ' Invalid Contact Phone. Please enter a 10-digit phone number.';
            }

            // Perform additional validation checks if needed

            return this.errMessage === ''; // Return true if no errors
        },
        submitForm() {
            if (this.validateForm()) {
                const apiUrl = 'https://mercury.swin.edu.au/cos30043/s103533680/api/api_application/apis_application.php';
                fetch(apiUrl, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(this.application)
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

                this.sucMessage = "Your registration has been submitted. We will catch you up soon!"
                this.resetForm();

            }
        },
        resetForm() {
            this.name = '';
            this.appliedPosition = '';
            this.appliedStore = '';
            this.contactEmail = '';
            this.contactPhone = '';
            this.personalDescription = '';
            this.errMessage = '';
        }
    },
    computed: {
        application() {
            return {
                name: this.name,
                appliedPosition: this.appliedPosition,
                store: this.appliedStore,
                contactEmail: this.contactEmail,
                contactPhone: this.contactPhone,
                personalDescription: this.personalDescription
            }
        }
    }
};
</script>