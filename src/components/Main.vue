<script setup>
    import Card from './Card.vue';
    import config from '../../config.json';
    

    let headersList = {
    "Accept": "*/*",
    "User-Agent": "Thunder Client (https://www.thunderclient.com)"
    }

    let response = await fetch(`https://oauth2.googleapis.com/token?client_id=${config.clientId}&client_secret=${config.clientSecret}&refresh_token=${config.refreshToken}&grant_type=refresh_token`, { 
        method: "POST",
        headers: headersList
    })

    let data = await response.text();
    const token = JSON.parse(data).access_token

    headersList["Authorization"] = 'Bearer ' + token

    let response2 = await fetch("https://photoslibrary.googleapis.com/v1/mediaItems", { 
        method: "GET",
        headers: headersList
    })


    const images = JSON.parse(await response2.text()).mediaItems
    console.log(images)
</script>

<template>
    <div v-for="image in images" class="">
      <Card :imgSrc=image.baseUrl></Card>
    </div>
</template>