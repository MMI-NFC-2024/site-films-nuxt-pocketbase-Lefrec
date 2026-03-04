<script setup lang="ts">
    const route = useRoute();
    const id = route.params.id as string;
    const nuxtApp = useNuxtApp();
    const film = await nuxtApp.$pb.collection("film").getOne(id);
</script>

<template>
    <NuxtLink to="/films">Retour</NuxtLink>
    <h1 class="text-4xl">{{ film.titre }}</h1>
    <NuxtLink :to="{name:'films-edit-id', params: {id:id}}">Modifier</NuxtLink>
</template>