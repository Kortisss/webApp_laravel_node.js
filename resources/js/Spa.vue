<template>
    <div class="container">
        Spa component <br/>
        <error/>
        <navigation/>
        <router-view></router-view>
    </div>
</template>
<script>

import Navigation from './components/Navigation.vue';
import Error from './components/Error.vue';

export default {
    inject: ["auth", "eventBus"],
    components: { Navigation, Error },
    created() {
        axios.interceptors.response.use(
            response => { return response; },
            error => {
                if (error.response.status === 401) {
                    this.eventBus.$emit("error");
                    this.auth.reset();
                }
                return Promise.reject(error);
            }
        );
    }
};

</script>