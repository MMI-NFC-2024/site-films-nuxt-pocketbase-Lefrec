<script setup lang="ts">
    const nuxtApp = useNuxtApp();
    const route = useRoute();
    const id = route.params.id as string;
    console.log(id);
    const film = ref({} as FilmResponse);

    onMounted(async () => {
        film.value = await nuxtApp.$pb.collection("film").getOne(id);
        film.value.date_sortie = (new Date(film.value.date_sortie)).toISOString().split("T")[0] as string;
    })

    async function editFilm(){
        if (id) {
            const editedFilm = await nuxtApp.$pb.collection("film").update(id,{
                ...film.value, 
                user: nuxtApp.$user.value?.id
            });
            if (editedFilm) {
                useRouter().push({name: 'films-id', params: {id: editedFilm.id}})
            }
        } else {
            const newFilm = await nuxtApp.$pb.collection("film").create({
                ...film.value, 
                user: nuxtApp.$user.value?.id
            });
            if (newFilm) {
                useRouter().push({name: 'films-id', params: {id: newFilm.id}})
            }
        }
        
    }
</script>

<template>
    <h1 v-if="id=='ajouter'" class="text-4xl">Ajouter</h1>
    <h1 v-else class="text-4xl">Modifier</h1>
    <form @submit.prevent="editFilm">
        <label>Titre
            <input type="text" v-model="film.titre">
        </label>
        <label>Date de sortie
            <input type="date" v-model="film.date_sortie">
        </label>
        <label>Synopsis
            <input type="text" v-model="film.synopsis">
        </label>
        <label>Durée (en minute)
            <input type="number" v-model="film.duree">
        </label>
        <button submit>Envoyer</button>
    </form>
</template>