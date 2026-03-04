<script setup lang="ts">
    const nuxtApp = useNuxtApp();
    async function loginGitHub() {
        const authData = await nuxtApp.$pb.collection("users").authWithOAuth2({provider: "github"})
        console.log("[loginGitHub] authData : ",authData)
    }
    const user = nuxtApp.$user;
</script>

<template>
    <button v-if="user" @click="nuxtApp.$pb.authStore.clear">Se déconnecter {{ user?.name || user?.email }}</button>
    <button v-else @click="loginGitHub">Se connecter avec GitHub</button>
</template>