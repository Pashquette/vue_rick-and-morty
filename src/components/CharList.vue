<template>
    <div className="charList__container">
        <div className="charList__title">
            <img src="../assets/header.png" alt="logo"/>
        </div>
        <CharSort v-model="selectedSort" :options="sortOptions"/>
        <div v-if="!isLoading">
            <CharLoader/>
        </div>
        <ul className="charList__list" v-else>
            <CharItem
                :character="character"
                v-for="character in sortedCharacters"
                :key="character.id"
                @open-modal="openModal"
            />
        </ul>
        <CharModal :show="showModal" :character="selectedCharacter" @close="closeModal"/>
    </div>
</template>

<script>
import CharItem from "@/components/CharItem.vue";
import CharLoader from "@/components/UI/CharLoader.vue";
import CharModal from "@/components/CharModal.vue";
import CharSort from "@/components/CharSort.vue";

export default {
    components: {CharLoader, CharItem, CharModal, CharSort},
    props: {
        characters: {
            type: Array,
            required: true
        },
        isLoading: {
            type: Boolean,
            required: true
        }
    },
    data() {
        return {
            showModal: false,
            selectedCharacter: null,
            selectedSort: '',
            sortOptions: [
                {value: 'default', name: 'По умолчанию'},
                {value: 'name', name: 'По имени'},
                {value: 'gender', name: 'По полу'},
                {value: 'location', name: 'По происхождению'},
            ]
        };
    },
    methods: {
        openModal(character) {
            this.selectedCharacter = character;
            this.showModal = true;
        },
        closeModal() {
            this.showModal = false;
        },
        sortCharacters() {
            if (this.selectedSort === 'location') {
                return [...this.characters].sort((char1, char2) => {
                    const name1 = char1.location.name || '';
                    const name2 = char2.location.name || '';
                    return name1.localeCompare(name2);
                });
            } else if (this.selectedSort === 'default') {
                return [...this.characters];
            } else {
                return [...this.characters].sort((char1, char2) => {
                    return char1[this.selectedSort]?.localeCompare(char2[this.selectedSort]);
                });
            }
        }
    },
    computed: {
        sortedCharacters() {
            return this.sortCharacters();
        }
    },
    watch: {
        selectedSort() {
            this.sortedCharacters = this.sortCharacters();
        }
    }
};
</script>

<style scoped>
.charList__container {
    background-color: #2f2f2f;
    color: #ffffff;
    font-family: 'Arial', sans-serif;
    padding: 20px;
    align-items: center;
}

.charList__title {
    text-align: center;
}

.charList__list {
    list-style: none;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(25%, 1fr));
    gap: 20px;
}
</style>
