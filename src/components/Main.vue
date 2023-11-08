<template>
    <div class="pa-3">
        <home-page  v-if="inHomePage"/>
        <about-page v-else-if="inAboutPage"/>
    </div>
</template>


<script>
    import { defineComponent } from 'vue';
    import HomePage      from "../pages/HomePage.vue";
    import AboutPage     from "../pages/AboutPage.vue";

    export default defineComponent({
        name: "Main",

        /** DATA */
        data() {
            return {

            }
        },

        /** PROPS */
        props: {
            page: {
                type    : String,
                required: true
            }
        },

        /** COMPONENTS */
        components: {
            'home-page'      : HomePage,
            'about-page'     : AboutPage
        },

        /** COMPUTED PROPERTIES */
        computed: {
            /**
             * Computed page is 'home' or not.
             * @returns {boolean}
             */
            inHomePage() {
                return this.page === 'home';
            },

            /**
             * Computed page is 'about' or not.
             * @returns {boolean}
             */
            inAboutPage() {
                return this.page === 'about';
            },
        }
    })
</script>


<style scoped>

</style>
