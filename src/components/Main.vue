<script setup>
    import Card from './Card.vue';
    import config from '../../config.json';

    let headersList = {
    "Accept": "*/*",
    "User-Agent": "Vue Malachi/1.0 (https://github.com/Skux4life/malachi)",
    "Content-Type": "application/json"
    }

    let response = await fetch(`https://oauth2.googleapis.com/token?client_id=${config.clientId}&client_secret=${config.clientSecret}&refresh_token=${config.refreshToken}&grant_type=refresh_token`, { 
        method: "POST",
        headers: headersList
    })

    let data = await response.text();
    const token = JSON.parse(data).access_token

    headersList["Authorization"] = 'Bearer ' + token

    let bodyContent = JSON.stringify({
        "pageSize": "100",
        "albumId": config.albumIdMalachi
    })

    let response2 = await fetch("https://photoslibrary.googleapis.com/v1/mediaItems:search", { 
        method: "POST",
        body: bodyContent,
        headers: headersList
    })


    const images = JSON.parse(await response2.text()).mediaItems
    console.log(images)
</script>

<template>
    <div class="wrapper">
        <div v-for="image in images" >
            <Card :imgSrc=image.baseUrl></Card>
        </div>
    </div>
</template>

<style scoped>
    .wrapper {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        place-items: center;
    }
</style>
