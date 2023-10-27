<template>
    <div class="charModal__container" v-if="show" @click="closeModal">
        <div class="charModal__content" @click.stop>
            <div class="charModal__content_image">
                <img :src="character.image" :alt="character.name" />
            </div>
            <div class="charModal__content_descr" v-if="character">
                <h2>{{ character.name }}</h2>
                <p><strong>Раса:</strong> {{ character.species }}</p>
                <p><strong>Пол:</strong> {{ character.gender }}</p>
                <p><strong>Статус:</strong> <span :class="statusClass">{{ character.status }}</span></p>
                <p><strong>Локация:</strong> {{ character.location.name }}</p>
            </div>
            <button @click="closeModal" class="charModal__close-btn"></button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        show: {
            type: Boolean,
            default: false
        },
        character: Object,
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
        closeModal() {
            this.$emit("close", false);
        },
    },
};
</script>

<style scoped>
.charModal__container {
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.5);
    position: fixed;
    display: flex;
    justify-content: center;
    align-items: center;
}

.charModal__content {
    position: relative;
    background: #78b03f;
    color: #2f2f2f;
    padding: 20px;
    border-radius: 12px;
    min-height: 600px;
    min-width: 600px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.charModal__content_image img {
    border-radius: 15px;
    margin-top: 20px;
}

.charModal__content_descr {
    text-align: center;
    margin-top: 20px;
}

.charModal__content_descr p {
    font-size: 18px;
    margin: 10px 0;
}

.charModal__content_descr strong {
    margin-right: 10px;
}

.alive-status {
    color: teal;
}

.dead-status {
    color: tomato;
}

.default-status {
    color: #2f2f2f
}

.charModal__close-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    width: 30px;
    height: 30px;
    background: none;
    border-radius: 50%;
    border: 1px solid black;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
}

.charModal__close-btn::before,
.charModal__close-btn::after {
    content: "";
    position: absolute;
    width: 2px;
    height: 14px;
    background: black;
}

.charModal__close-btn::before {
    transform: rotate(45deg);
}

.charModal__close-btn::after {
    transform: rotate(-45deg);
}
</style>
