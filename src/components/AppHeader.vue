<template>
    <v-card>
        <v-tabs grow class="d-flex" bg-color="#B7E4C7" color="#40916C" v-model="activeTab" align-tabs="center" center-active stacked>
            <v-tab elevation="1" to="/"><v-icon icon="mdi-home" color="#081C15"></v-icon></v-tab>
            <v-tab elevation="1" to="/componentOne">Menu</v-tab>
            <v-tab elevation="1" to="/componentTwo">Review</v-tab>
            <v-tab elevation="1" to="/componentThree">Careers</v-tab>
            <v-tab elevation="1" to="/componentFour">Admin</v-tab>
        </v-tabs>
    </v-card>
</template>
<script>
export default {
    name: 'AppHeader',
    data() {
        return {
            activeTab: null
        };
    }
};
</script>