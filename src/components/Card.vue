<script setup>
    defineProps(['imgSrc'])
</script>

<template>
    <div class="frame">
        <img :src="imgSrc" />
    </div>
</template>

<style scoped>
img {
    width: 100%;
    height: 100%;
}

.frame {
    width: 400px;
    margin: 1em;
    border: 3px solid #ccc;
    background: #eee;
    padding: 5px 10px;
}
</style>