<template>
    <v-card-item v-if="!authenticated">
        <v-card-title>Admin Login</v-card-title>
        <v-card-text class="my-4">
            <v-sheet max-width="500" class="mx-auto">
                <v-form class="border elevation-4 rounded-lg p-3">
                    <v-text-field v-model="username" label="Username" outlined></v-text-field>
                    <v-text-field v-model="password" :append-icon="showPasswordInPlainText ? 'mdi-eye' : 'mdi-eye-off'"
                        :type="showPasswordInPlainText ? 'text' : 'password'" name="input-10-1" label="Password" counter
                        @click:append="showPasswordInPlainText = !showPasswordInPlainText" outlined></v-text-field>
                    <v-alert v-if="errMessage !== ''" color="#ffccd5" type="error" title="Invalid Credentials" :text="errMessage"></v-alert>
                    <v-btn @click="login()" type="button" class="mt-2" text="Login" block></v-btn>
                </v-form>
            </v-sheet>
        </v-card-text>
    </v-card-item>
    <v-card-item v-else>
        <AdminDashboard></AdminDashboard>
    </v-card-item>
</template>
<script>
import AdminDashboard from './AdminDashboard.vue';
import 'bootstrap/dist/css/bootstrap.css';


export default {
    name: 'ComponentFour',
    components: {
        AdminDashboard
    },
    data() {
        return {
            showPasswordInPlainText: false,
            username: '',
            password: '',
            authenticated: false,
            errMessage: ''
        }
    },
    methods: {
        login() {
            // Send a POST request to the API for validation
            fetch('https://mercury.swin.edu.au/cos30043/s103533680/api/api_user/api_user.php', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(this.credential)
            })
                .then(response => {
                    return response.json()
                })
                .then(data => {
                    if (data == null) {
                        console.log("Authentication failed")
                        this.errMessage = 'Please try again.'
                    } else {
                        console.log("Logon successful")
                        this.authenticated = true;
                    }
                })
                .catch(error => {
                    console.error('An error occurred during form validation:', error);
                });
            this.username = '';
            this.password = '';
        }
    },
    computed: {
        credential() {
            return {
                username: this.username,
                password: this.password
            }
        }
    }
};
</script>