<template>
    <div id="app">
<!--        <transition name="slide-fade">-->
<!--      <span>-->
<!--    <circle-loading :loading="testt" @update-cart="zmiana"/>-->
<!--      </span>-->
<!--        </transition>-->


        <transition name="slide-fade">

            <FlexContainer class="full-h-w ss-justify-center ss-align-center"   v-show="show">
                <box-flex data-aos="fade-left" class="img-phone"><img src="./assets/images/2.jpg"  style="width:100%;" alt=""></box-flex>
                <box-flex data-aos="fade-right"  class="img-phone"><img src="./assets/images/2.jpg"  style="width:100%;" alt=""></box-flex>
                <box-flex data-aos="fade-left"  class="img-phone"><img src="./assets/images/2.jpg"  style="width:100%;" alt=""></box-flex>
                <box-flex  data-aos="fade-rigth"  class="img-phone"><img src="./assets/images/2.jpg"  style="width:100%;" alt=""></box-flex>
            </FlexContainer>


        </transition>
        <router-view></router-view>

    </div>
</template>

<style lang="scss">

</style>
<script>
    import CircleLoading from "./components/CircleLoading";
    import FlexContainer from "./components/FlexContainer";
    import ImgContainer from "./components/imgContainer";
    import BoxFlex from "./components/BoxFlex";

    export default {
        data() {
            return {
                testt: true,
                show: true,
                url: '/img/',
                jpg: '.jpg'
            }
        },
        components: {BoxFlex, ImgContainer, FlexContainer, CircleLoading},
        methods: {
            zmiana() {
                this.testt = false
                setTimeout(() =>     this.show = true, 2000);

            }
        },

    }
</script>

<style>
    #app {
        color: white;
        min-height: 100vh;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: black;
    }

    /* Enter and leave animations can use different */
    /* durations and timing functions.              */
    .slide-fade-enter-active {
        transition: all .3s ease;
    }

    .slide-fade-leave-active {
        transition: all 0.8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }

    .slide-fade-enter, .slide-fade-leave-to
        /* .slide-fade-leave-active below version 2.1.8 */
    {
        transform: translateX(10px);
        opacity: 0;
    }
</style>