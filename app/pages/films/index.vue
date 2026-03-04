<script setup lang="ts">
    const nuxtApp = useNuxtApp();
    const films = await nuxtApp.$pb.collection("film").getFullList();
</script>

<template>
    <h1 class="text-4xl">Liste des films</h1>
    <ul>
        <li v-for="film in films">
            <NuxtLink :to="{name:'films-id', params: {id:film.id}}">{{ film.titre }}</NuxtLink>
        </li>
    </ul>
    <NuxtLink to="/films/edit/ajouter">Ajouter un film</NuxtLink>
</template>