<template>
    <transition name="fade">
<div class="loading__container" v-if="loading">
    <img src="../assets/images/11.png" />

   <h1 class="enter" @click="changeHandle" >ENTER</h1>

</div>
    </transition>
</template>

<script>
    export default {
        props: {
            loading: { type: Boolean,
            default: true,}
        },
        name: "CircleLoading",
        data() {
            return {

            }
        },
        methods: {
            changeHandle() {
                this.$emit('update-cart')
            }
        }
    }
</script>

<style scoped lang="scss">
    .loading__container {

        height: 600px;
        text-align: center;
        display: flex;
        flex-direction: column;
        align-content: space-between;
        cursor: pointer;
    }

            img {
                /*position: absolute*/
                margin: auto;
                width: 350px;
                height: 300px;
                animation:spin 4s linear infinite;

            }
            .enter {
                color:white;

                letter-spacing: 15px;
            }

    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
            @keyframes spin { 100% { -webkit-transform: rotate(360deg); transform:rotate(360deg); } }
</style>