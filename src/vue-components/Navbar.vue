<template>
    <section class="overlay">

        <div class="overlay__section overlay__section--primary">
            <h1 class="overlay__title fs-m fw-bold">
                Lomas Brewing
            </h1>
            <ul class="overlay__nav">
                <li class="overlay__nav-item fs-s" v-for="nav_item in nav_items" :class="{ 'active' : nav_item.active }">
                    <a href="#">{{ nav_item.name }}</a>
                </li>
            </ul>
        </div>

        <div class="overlay__section overlay__section--secondary wysiwyg-content">
            <p class="fw-bold fs-s">Lomas Brewing Company right reserved some other company bullshit idk</p>
            <p class="fs-s">
                <a href="http://eddsmith.com/" target="_blank" rel="noopener">Made by eddsmith.com</a>
            </p>
        </div>

        <div class="overlay__section overlay__section--tertiary">
            <ul class="overlay__social">
                <li class="overlay__social-item" v-for="social_item in social_items">
                    <a :href="social_item.url">
                        <i class="fab" :class="'fa-' + social_item.name"></i>
                    </a>
                </li>
            </ul>
        </div>

    </section>
</template>

<script>

    export default {
        name: 'navbar',

        props: {
            nav_items: Array,
            social_items: Array
        },

        methods: {

        },

        data () {
            return {
            }
        },

        methods: {
            set_active_nav_item ( nav_item ) {
                this.nav_items.find( nav_item => nav_item.active == true ).active = false;
                nav_item.active = true;
            }
        }
    };
</script>

<style lang="scss">
    @import "./../scss-components/_global.scss";

    .overlay {
        color: map-get( $colours, 'white' );
        position: relative;
        z-index: 1;
        mix-blend-mode: difference;

        &__section {
            @include from-to-with-between( 'padding', 20px, 40px );
            position: fixed;

            &--primary {
                width: 100%;
                top: 0;
                left: 0;
                display: flex; 
                justify-content: space-between;
                
                @media ( min-width: 768px ) {
                    align-items: center;
                }    
            }

            &--secondary {
                display: none;
                position: fixed;
                width: 100%;
                bottom: 0;
                left: 0;
                width: 50%;

                @media ( min-width: 768px ) {
                    display: block;
                }
            }

            &--tertiary {
                display: none;
                transform: translateY(-50%);
                right: 0;
                top: 50%;

                @media ( min-width: 768px ) {
                    display: block;
                }
            }
        }

        &__title {
            font-size: $base-font-size;
        }

        &__nav {
            list-style: none;

            @media ( min-width: 768px ) {
                display: flex;
            }
        }

        &__nav-item {
            text-align: right;

            &:not(:last-child) {
                margin-bottom: 10px;

                @media ( min-width: 768px ) {
                    margin-bottom: 0;
                    margin-right: 20px;
                }
            }

            a {
                display: block;
            }

            // &.active {
            //     border-bottom: 3px solid map-get($colours, 'white');
            // }
        }

        &__social {
            list-style: none;
        }

        &__social-item {
            &:not(:last-child) {
                margin-bottom: 20px;
            }   
        }
    }
</style>
