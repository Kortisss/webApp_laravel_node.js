<template>
    <div class="m-3">
        <h1>Login component</h1>
        <form>
            <div>
                <label for="email">email:</label>
                <input v-model="form.email" type="email" id="email"/>
            </div>
            <div>
                <label for="password">hasło:</label>
                <input v-model="form.password" type="password" id="password"/>
            </div>
            <button @click.prevent="login">zaloguj sie</button>
        </form>
    </div>
</template>
<script>
export default {
    inject: ["auth"],
    data() {
        return {
            form: {
                email: "",
                password: ""
            }
        };
    },
    methods: {
        async login() {
            try {
                await this.auth.login(this.form);
            } catch (err) {
                this.form.email = "";
                this.form.password = "";
            }
        }
    }
};
</script>