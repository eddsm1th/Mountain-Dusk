<template>
    <main>

        <!-- <splashscreen></splashscreen> -->

        <overlay></overlay>

        <hero></hero>

        <about></about>

        <showcase></showcase>

    </main>
</template>

<script>

    import Overlay from './vue-components/Overlay.vue';
    import Hero from './vue-components/Hero.vue';
    import About from './vue-components/About.vue';
    import Showcase from './vue-components/Showcase.vue';
    import Splashscreen from './vue-components/Splashscreen.vue';

    export default {
        name: 'app',

        components: {
            Overlay,
            Hero,
            About,
            Showcase,
            Splashscreen
        },

        data () {
            return {
            }
        }
    };
</script>

<style lang="scss">
    @import "./scss-components/_global.scss";

    *, *:after, *:before {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
        font-weight: 400;
    }

    a {
        &, &:active, &:hover {
            color: inherit;
            text-decoration: none;
        }
    }

    html {
        font-family: 'Montserrat', sans-serif;
        font-size: $base_font-size;
    }

    body {
        background-color: map-get( $colours, 'grey-dark' );
        min-height: 100vh;
    }
</style>
