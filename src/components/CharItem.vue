<template>
    <div class="character-card">
        <div class="character-card-inner">
            <div class="character-image">
                <img :src="character.image" :alt="character.name" />
            </div>
            <div class="character-details">
                <h2>{{ character.name }}</h2>
                <p class="character-info">Пол: {{ character.gender }}</p>
                <p class="character-info">Статус: {{ character.status }}</p>
                <p class="character-info">Локация: {{ character.location.name }}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        characters: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
    /* Стили для character-card (каждой карточки) */
    .character-card {
        border: 1px solid #4d505c;
        border-radius: 15px;
        display: flex;
        flex-direction: row;
        max-width: 100%;
        margin-bottom: 20px;
    //box-shadow: 0 8px 16px rgba(153, 245, 56, 0.68);
        transition: transform 0.3s, box-shadow 0.3s;
    }

    .character-card:hover {
        cursor: pointer;
        transform: translate(0, -10px); /* Поднимаем карточку вверх */
        box-shadow: 0 8px 16px rgba(153, 245, 56, 0.68);
    }

    .character-card-inner {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        min-height: 200px;
    }

    /* Остальные стили остаются без изменений */
    .character-image {
        border-top-left-radius: 15px;
        border-bottom-left-radius: 15px;

        overflow: hidden;
        max-width: 100%;
        max-height: 200px;
    }
    .character-image img {
        max-height: 100%;
    }

    .character-details {
        flex: 1;
    }

    .character-info {
        margin: 4px 0;
        font-size: 14px;
    }
</style>