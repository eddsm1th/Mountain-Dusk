<template>
    <section class="showcase" :class="transition_class">
        <div class="section-wrap">
            <div class="showcase__inner-wrap">

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
                        <img :src="current_item.image_url">
                    </div>
                    <div class="showcase__content">
                        <div>
                            <div class="showcase__content-upper">
                                <h3 class="showcase__title fs-xl fw-bold">{{ current_item.name }}</h3>
                                <h4 class="showcase__sub-title fs-l fw-bold">{{ current_item.short_description }}</h4>
                            </div>
                            <div class="showcase__body-content wysiwyg-content" v-html="current_item.description"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>

    export default {
        name: 'showcase',

        data () {
            return {
                brews: [
                    {
                        'name' : 'Golden Meadow',
                        'short_description' : 'German Inspired Lager',
                        'description' : `<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non.</p><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non.</p>`,
                        'image_url' : 'http://via.placeholder.com/280x420.png?text=Golden+Meadow'
                    },
                    {
                        'name' : 'Mountain Dusk',
                        'short_description' : 'Japanese Inspired Lager',
                        'description' : `<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum, in eleifend risus sodales non.</p><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas cursus nulla ac viverra congue. Maecenas vulputate erat ipsum.</p>`,
                        'image_url' : 'http://via.placeholder.com/280x420.png?text=Mountain+Dusk'
                    }
                ],
                active_item: 1,
                transition_class: '',
                transition_classes: {
                    out: 'transition-out',
                    in: 'transition-in',
                    idle: ''
                },
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
                    this.transition_class = this.transition_classes.out;
                    this.can_transition = false;

                    setTimeout( function () {
                        this.active_item += difference;

                        if ( this.active_item < 1 ) this.active_item = this.brews.length;
                        if ( this.active_item > this.brews.length ) this.active_item = 1;

                        this.transition_class = this.transition_classes.in;

                        setTimeout( function () {
                            this.can_transition = true;
                            this.transition_class = this.transition_classes.idle;
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
        overflow: hidden;

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
                width: 1.2em;
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
            flex-wrap: wrap;
            position: relative;
        }

        &__image {
            width: 100%;
            position: relative;
            max-width: 320px;
            padding-right: 40px;

            @media ( min-width: 580px ) {
                padding-right: 80px;
            }

            @media ( min-width: 940px ) {
                padding-right: 0;
                width: 35%;
            }

            > img {
                // position: relative;
                top: 0;
                left: 0;
                width: 100%;
                display: block;
            }

            .transition-out & {
                @include transition-out();
            }
            .transition-in & {
                @include transition-in();
            }
        }

        &__content {
            width: 100%;
            padding: 20px 0 20px 40px;
            display: flex;
            align-items: center;
            position: relative;

            @media ( min-width: 580px ) {
                padding: 20px 0 20px 80px;
            }

            @media ( min-width: 940px ) {
                width: 65%;
                padding: 40px 40px 40px 40px;
            }

            @media ( min-width: 1024px ) {
                padding: 40px 40px 40px 80px;
            }
        }

        &__content-upper {
            position: absolute;
            bottom: 100%;
            left: 40px;

            @media ( min-width: 580px ) {
                left: 80px;
            }

            @media ( min-width: 940px ) {
                position: static;
            }
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
            margin-bottom: 20px;
            animation-delay: .2s;

            @media ( min-width: 940px ) {
                margin-bottom: 40px;
            }

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
