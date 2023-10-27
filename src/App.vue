<template>
    <div class="app">
        <CharList :characters="characters" :isLoading="isLoading" @open-modal="showModal" />
        <CharModal v-model:show="modalVisible" :character="selectedCharacter" @close="closeModal" />
    </div>
</template>

<script>
import CharList from "@/components/CharList.vue";
import CharModal from "@/components/CharModal.vue";

export default {
    components: {
        CharModal,
        CharList
    },
    data() {
        return {
            characters: [],
            isLoading: true,
            modalVisible: false,
            selectedCharacter: null
        };
    },
    created() {
        this.fetchAllCharacters();
    },
    methods: {
        async fetchAllCharacters() {
            try {
                let page = 1;
                let allCharacters = [];
                let hasMore = true;
                this.isLoading = false;

                while (hasMore) {
                    const response = await fetch(`https://rickandmortyapi.com/api/character/?page=${page}`);
                    const data = await response.json();

                    if (data.results && data.results.length > 0) {
                        allCharacters = allCharacters.concat(data.results);
                        page++;
                    } else {
                        hasMore = false;
                        this.isLoading = true;
                    }
                }
                this.characters = allCharacters;
            } catch (error) {
                console.error('Ошибка при получении данных:', error);
            }
            console.log(this.characters);
        },
        showModal(character) {
            this.selectedCharacter = character;
            this.modalVisible = true;
        },

        closeModal() {
            this.modalVisible = false;
        }
    }
};
</script>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
</style>