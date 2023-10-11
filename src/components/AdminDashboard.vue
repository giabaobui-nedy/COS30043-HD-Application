<template>
    <v-card-title>Admin Dashboard</v-card-title>
    <div v-if="loading">Loading...</div>
    <div v-else>
        <v-card-item title="Recent Applications">
            <v-card class="m-4 p-3" v-for="application in applications" :key="application.id">
                <v-card-title>Application {{ application.id }}</v-card-title>
                <v-card-subtitle>Position: {{ application.appliedPosition }}. Store: {{ application.store
                }}</v-card-subtitle>
                <v-card-text>
                    <div>
                        Applicant's name: {{ application.NAME }}
                    </div>
                    <div>
                        Applicant's contact email: {{ application.contactEmail }}
                    </div>
                    <div>
                        Applicant's contact phone: {{ application.contactPhone }}
                    </div>
                    <div>
                        Applicant's description: {{ application.personalDescription }}
                    </div>
                </v-card-text>
            </v-card>
        </v-card-item>
    </div>
</template>

<script>
import axios from 'axios';
import 'bootstrap/dist/css/bootstrap.css';

export default {
    name: 'AdminDashboard',
    data() {
        return {
            applications: [],
            loading: true
        };
    },
    mounted() {
        this.fetchApplications();
    },
    methods: {
        fetchApplications() {
            axios
                .get('https://mercury.swin.edu.au/cos30043/s103533680/api/api_application/apis_application.php')
                .then(response => {
                    this.applications = response.data;
                    this.applications.reverse();
                    this.loading = false;
                })
                .catch(error => {
                    console.error('Failed to fetch applications:', error);
                    this.loading = false;
                });
        }
    }
};
</script>
  