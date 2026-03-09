<script setup lang="ts">
    const route = useRoute();
    const id = route.params.id as string;
    const nuxtApp = useNuxtApp();
    const personne = await nuxtApp.$pb.collection("personne").getOne(id);
</script>

<template>
    <NuxtLink to="/personnes">Retour</NuxtLink>
    <h1 class="text-4xl">{{ personne.prenom }} {{ personne.nom }}</h1>
    <NuxtLink :to="{name:'personnes-edit-id', params: {id:id}}">Modifier</NuxtLink>
</template>