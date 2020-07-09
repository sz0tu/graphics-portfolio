<template>
    <div class="container">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        name: "FlexContainer"
    }
</script>

<style scoped>

    .container {
        display: flex;
        flex-wrap: wrap;
        height: 100%;

    }

</style>