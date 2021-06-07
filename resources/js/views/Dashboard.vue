<template>
    <div>
        Spa Dashboard
        <div v-if="user">Zalogowany użytkownik: {{user}} </div>
    </div>
</template>
<script>
export default {
    inject: ["auth"],
    data() {
        return {
            user: null
        };
    },
    created() {
        this.getAuthUser();
    },
    methods: {
        async getAuthUser() {
            let user = await this.auth.getAuthUser();
            this.user = user.data.name;
        }
    }
};
</script>