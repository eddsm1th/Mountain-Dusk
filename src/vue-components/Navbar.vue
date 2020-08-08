<template>
        <ul class="nav">
            <li class="nav__item fs-s"
                v-for="nav_item in nav_items"
                :class="{ 'active' : nav_item.active }"
                @click="set_active_nav_item( nav_item )"
            >
                <a href="#">{{ nav_item.name }}</a>
            </li>
        </ul>
</template>

<script>

    export default {
        name: 'navbar',

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
                    }
                ]
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

    .nav {
        list-style: none;

        @media ( min-width: 768px ) {
            display: flex;
        }

        &__item {
            text-align: right;

            &:not(:last-child) {
                margin-bottom: 20px;

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
    }
</style>
