<template>
    <main>

        <navbar :nav_items="nav_items" :social_items="social_items"></navbar>

        <hero></hero>

        <about></about>

        <showcase></showcase>

    </main>
</template>

<script>

    import Navbar from './vue-components/Navbar.vue';
    import Hero from './vue-components/Hero.vue';
    import About from './vue-components/About.vue';
    import Showcase from './vue-components/Showcase.vue';

    export default {
        name: 'app',

        components: {
            Navbar,
            Hero,
            About,
            Showcase
        },

        methods: {

        },

        data () {
            return {
                nav_items: [
                    {
                        'name' : 'Home',
                        'url' : 'home',
                        'active' : true,
                    },
                    {
                        'name' : 'Who are we',
                        'component_name' : 'WhoWeAre',
                        'url' : 'who-are-we',
                        'active' : false,
                    },
                    {
                        'name' : 'Philosophy',
                        'url' : 'philosophy',
                        'active' : false,
                    },
                    {
                        'name' : 'Contact',
                        'url' : 'Contact',
                        'active' : false,
                    },

                ],
                social_items: [
                    {
                        'name' : 'instagram',
                        'url' : '#'
                    },
                    {
                        'name' : 'twitter',
                        'url' : ''
                    },
                    {
                        'name' : 'facebook',
                        'url' : '#'
                    }
                ]
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
