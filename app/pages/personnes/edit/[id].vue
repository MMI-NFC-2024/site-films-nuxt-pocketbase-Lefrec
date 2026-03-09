<script setup lang="ts">
    const nuxtApp = useNuxtApp();
    const route = useRoute();
    const id = route.params.id as string;
    console.log(id);
    const personne = ref({} as PersonneResponse);

    onMounted(async () => {
        if (id != 'ajouter') {
            personne.value = await nuxtApp.$pb.collection("personne").getOne(id);
            personne.value.date_naissance = (new Date(personne.value.date_naissance)).toISOString().split("T")[0] as string;
            personne.value.date_deces = (new Date(personne.value.date_deces)).toISOString().split("T")[0] as string;
        }
    })

    async function editPersonne(){
        if (id != 'ajouter') {
            const editedPersonne = await nuxtApp.$pb.collection("personne").update(id,{
                ...personne.value, 
                user: nuxtApp.$user.value?.id
            });
            if (editedPersonne) {
                useRouter().push({name: 'personnes-id', params: {id: editedPersonne.id}})
            }
        } else {
            const newPersonne = await nuxtApp.$pb.collection("personne").create({
                ...personne.value, 
                user: nuxtApp.$user.value?.id
            });
            if (newPersonne) {
                useRouter().push({name: 'personnes-id', params: {id: newPersonne.id}})
            }
        }
        
    }
</script>

<template>
    <h1 v-if="id=='ajouter'" class="text-4xl">Ajouter</h1>
    <h1 v-else class="text-4xl">Modifier</h1>
    <form @submit.prevent="editPersonne">
        <label>Prenom
            <input type="text" v-model="personne.prenom">
        </label>
        <label>Nom
            <input type="text" v-model="personne.nom">
        </label>
        <label>Nationalité
            <input type="text" v-model="personne.nationalite">
        </label>
        <label>Date de naissance
            <input type="date" v-model="personne.date_naissance">
        </label>
        <label>Date de décès
            <input type="date" v-model="personne.date_deces">
        </label>
        <label>Profession
            <select multiple="true" v-model="personne.profession">
                <option v-for="profession in PersonneProfessionOptions">{{ profession }}</option>
            </select>
        </label>
        <button submit>Envoyer</button>
    </form>
</template>