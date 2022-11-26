<script setup>
    defineProps(['imgSrc'])
</script>

<template>
    <div>
        <img :src="imgSrc" width="400" />
    </div>
</template>

<style scoped>
img {
    margin: 2em
}
</style>