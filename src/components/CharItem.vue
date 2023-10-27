<template>
    <div class="charItem__container" @click="openModal">
        <div class="charItem__inner">
            <div class="charItem__image">
                <img :src="character.image" :alt="character.name" />
            </div>
            <div class="charItem__details">
                <h2>{{ character.name }}</h2>
                <p class="charItem__info">Пол: {{ character.gender }}</p>
                <p class="charItem__info">Статус: <span :class="statusClass">{{ character.status }}</span></p>
                <p class="charItem__info">Локация: {{ character.location.name }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        character: {
            type: Object,
            required: true
        }
    },
    computed: {
        statusClass() {
            if (this.character.status === 'Alive') {
                return 'alive-status';
            } else if (this.character.status === 'Dead') {
                return 'dead-status';
            } else {
                return 'default-status';
            }
        }
    },
    methods: {
        openModal() {
            this.$emit("open-modal", this.character);
        }
    }
}
</script>

<style scoped>
    .charItem__container {
        border: 1px solid #4d505c;
        border-radius: 15px;
        display: flex;
        max-width: 100%;
        margin-bottom: 20px;
        transition: transform 0.3s, box-shadow 0.3s;
    }

    .charItem__container:hover {
        cursor: pointer;
        transform: translate(0, -10px);
        box-shadow: 0 8px 16px rgba(153, 245, 56, 0.68);
    }

    .charItem__inner {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        min-height: 0;
        //padding: 20px 0;
    }

    .charItem__image {
        border-top-left-radius: 15px;
        border-bottom-left-radius: 15px;

        overflow: hidden;
        max-width: 100%;
        max-height: 200px;
    }
    .charItem__image img {
        max-height: 100%;
    }

    .charItem__details {
        flex-grow: 1;
        margin-top: 10px;
        margin-left: 40px;
    }

    .charItem__info {
        margin: 4px 0;
        font-size: 16px;
    }

    .alive-status {
        color: #99F538AD;
    }

    .dead-status {
        color: tomato;
    }

    .default-status {
        color: #ffffff;
    }
</style>