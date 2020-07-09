<template>

    <img :src="picture_src" />

</template>

<script>
    export default {
        name: "ImgItem",
        props: {
            picture_src: String,
            pic_desc: String
        }
    }
</script>

<style scoped>

</style>