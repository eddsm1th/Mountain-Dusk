<template>
    <header class="hero">

        <div class="section-wrap section-wrap--wide hero__content">
            <h1 class="hero__heading" v-html="heading"></h1>
            <h2 class="hero__subheading fs-l" v-html="subheading"></h2>
        </div>

        <ul class="hero__ctas">
            <li class="hero__cta">
                <a href="#">
                    <span class="fs-xs">01</span>
                    <h3 class="fs-m">Our brews</h3>
                    <p class="fs-s">Find out more about our specialty brews</p>
                </a>
            </li>
            <li class="hero__cta">
                <a href="#">
                    <span class="fs-xs">02</span>
                    <h3 class="fs-m">Why us</h3>
                    <p class="fs-s">What does LomasBrewing do different</p>
                </a>
            </li>
        </ul>

    </header>
</template>

<script>

    export default {
        name: 'hero',

        props: {
        },

        methods: {

        },

        data () {
            return {
                heading: 'Lomas<br>Brewing.',
                subheading: 'Good beer, but even better stories...'
            }
        },
    };
</script>

<style lang="scss">
    @import "./../scss-components/_global.scss";

    $cta_dimension: 220px;


    .hero {
        min-height: 100vh;
        position: relative;
        display: flex;
        align-items: center;

        &__content {
            @include from-to-with-between( 'margin-top', ( $cta_dimension / -2 ) * .666, $cta_dimension / -2 );
            color: map-get($colours, 'white');
            line-height: 1;
        }

        &__heading {
            @include from-to-with-between( 'font-size', 48px, 96px, 320px, 768px );
            @include from-to-with-between( 'font-size', 96px, 120px, 768px, 1440px );
            font-weight: 900;
            margin-bottom: 24px;
            text-transform: uppercase;
        }

        &__ctas {
            list-style: none;
            position: absolute;
            bottom: 0;
            right: 0;
            width: 100%;
            background-color: map-get($colours, 'black');
            display: flex;
            flex-wrap: wrap;

            @media ( min-width: 768px ) {
                width: 50%;
            }
        }

        &__cta {
            width: 100%;

            @media ( min-width: 580px ) {
                width: 50%;
            }
            
            a {
                @include from-to-with-between( 'padding', 20px, 40px );
                @include from-to-with-between( 'height', $cta_dimension * .5, $cta_dimension );
                display: flex;
                flex-direction: column;
                align-items: flex-start;
                justify-content: center;    
                color: map-get($colours, 'white');

                > * {
                    position: relative;
                    z-index: 1;
                }

                > span {
                    margin-bottom: auto;
                }

                > h3 {
                    font-weight: 600;
                    margin-bottom: 12px;
                }
            }
        }
    }
</style>
