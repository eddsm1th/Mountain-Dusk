<template>
    <section class="showcase" :class="transition_class">
        <div class="showcase__inner-wrap section-wrap section-wrap--narrow">

            <div class="showcase__main">
                <div class="showcase__utils">
                    <div class="showcase__slide-indicator fs-s fw-bold">
                        <span class="fs-xl fw-bold">{{ normalised_current_item_index }}</span> / {{ normalised_item_length }}
                    </div>
                    <div class="showcase__controls" :class="{ 'disabled' : !can_transition }">
                        <span class="showcase__control showcase__control--prev" @click="cycle_active_item( -1 )"></span>
                        <span class="showcase__control" @click="cycle_active_item()"></span>
                    </div>
                </div>
                <div class="showcase__image">
                    <img src="http://via.placeholder.com/240x420.png">
                </div>
                <div class="showcase__content">
                    <div>
                        <h3 class="showcase__title fs-xl fw-bold">{{ current_item.name }}</h3>
                        <h4 class="showcase__sub-title fs-l fw-bold">{{ current_item.short_description }}</h4>
                        <div class="showcase__body-content wysiwyg-content" v-html="current_item.description"></div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>

    export default {
        name: 'showcase',

        props: {
        },

        methods: {

        },

        data () {
            return {
                brews: [
                    {
                        'name' : 'Golden Meadow',
                        'short_description' : 'German Inspired Lager',
                        'description' : `<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non.</p><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non.</p>`
                    },
                    {
                        'name' : 'Mountain Dusk',
                        'short_description' : 'Japanese Inspired Lager',
                        'description' : `<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non.</p><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non.</p>`
                    }
                ],
                active_item: 1,
                transition_class: '',
                can_transition: true,
            }
        },

        computed: {
            current_item () {
                return this.brews[ this.active_item - 1 ];
            },

            normalised_current_item_index () {
                return this.active_item < 10 ? ( '0' + this.active_item ) : this.active_item;
            },

            normalised_item_length () {
              return this.brews.length < 10 ? ( '0' + this.brews.length ) : this.brews.length;  
            }
        },

        methods: {
            cycle_active_item ( difference = 1 ) {
                if ( this.can_transition ) { 
                    this.transition_class = 'transition-out';
                    this.can_transition = false;

                    setTimeout( function () {
                        this.active_item += difference;

                        if ( this.active_item < 1 ) this.active_item = this.brews.length;
                        if ( this.active_item > this.brews.length ) this.active_item = 1;

                        this.transition_class = 'transition-in';

                        setTimeout( function () {
                            this.can_transition = true;
                            this.transition_class = '';
                        }.bind( this ), 800 );
                    }.bind( this ), 1000 );
                }
            }
        }
    };
</script>

<style lang="scss">
    @import "./../scss-components/_global.scss";

    .showcase {
        background-color: white;

        &__inner-wrap {
            min-height: 100vh;
            padding-top: 100px;
            padding-bottom: 100px;
            display: flex;
            align-items: center;
        }

        $utility_desktop_spacing: 12px;

        &__slide-indicator {
            position: absolute;
            bottom: 100%;
            left: 0;
            display: flex;
            margin-bottom: $utility_desktop_spacing;

            > span {
                line-height: 1;
                margin-right: 8px;
            }
        }

        &__controls {
            position: absolute;
            top: 100%;
            right: 0;
            margin-top: $utility_desktop_spacing * 1.22;
            display: flex;
            transition: .2s opacity ease-out;

            &.disabled {
                opacity: .4;
            }
        }

        &__control {
            $base_dimension: 20px;
            
            width: $base_dimension;
            height: $base_dimension;
            border-top: 3px solid map-get( $colours, 'black' );
            border-right: 3px solid map-get( $colours, 'black' );
            display: block;
            transform: rotate( 45deg );

            &--prev {
                margin-right: $base_dimension;
                transform: rotate( -135deg );
            }
        }

        &__main {
            display: flex;
            position: relative;
        }

        &__image {
            width: 35%;
            position: relative;

            > img {
                // position: relative;
                top: 0;
                left: 0;
                width: 100%;
            }

            .transition-out & {
                @include transition-out();
            }
            .transition-in & {
                @include transition-in();
            }
        }

        &__content {
            width: 65%;
            padding: 40px 0 40px 80px;
            display: flex;
            align-items: center;
        }

        &__title {
            animation-delay: .1s;

            .transition-out & {
                @include transition-out();
            }
            .transition-in & {
                @include transition-in();
            }
        }

        &__sub-title {
            margin-bottom: 40px;
            animation-delay: .2s;

            .transition-out & {
                @include transition-out();
            }
            .transition-in & {
                @include transition-in();
            }
        }

        &__body-content {
            animation-delay: .3s;
            
            .transition-out & {
                @include transition-out();
            }
            .transition-in & {
                @include transition-in();
            }
        }
    }
</style>
