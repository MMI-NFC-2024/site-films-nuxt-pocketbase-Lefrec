<script setup lang="ts">
    const nuxtApp = useNuxtApp();
    const personnes = await nuxtApp.$pb.collection("personne").getFullList();
</script>

<template>
    <h1 class="text-4xl">Liste des personnes</h1>
    <ul>
        <li v-for="personne in personnes">
            <NuxtLink :to="{name:'personnes-id', params: {id:personne.id}}">{{ personne.prenom }}{{ personne.nom }}</NuxtLink>
        </li>
    </ul>
    <NuxtLink to="/personnes/edit/ajouter">Ajouter un personne</NuxtLink>
</template>