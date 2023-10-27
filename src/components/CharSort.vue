<template>
    <div class="charSort__characters">
        <select :value="modelValue" @input="changeOption" class="charSort__select">
            <option disabled value="">Сортировка по...</option>
            <option
                v-for="option in options"
                :key="option.value"
                :value="option.value"
            >
                {{ option.name }}
            </option>
        </select>
    </div>
</template>

<script>
export default {
    props: {
        modelValue: {
            type: String,
        },
        options: {
            type: Array,
            default: () => [],
        },
    },
    methods: {
        changeOption(event) {
            this.$emit("update:modelValue", event.target.value);
        },
    },
};
</script>

<style scoped>
.charSort__characters {
    display: flex;
    align-items: center;
    width: 100%;
    margin-top: 20px;
    margin-bottom: 20px;
}

.charSort__select {
    flex: 1;
    padding: 10px;
    background-color: #2f2f2f;
    color: #ffffff;
    border: 2px solid #78b03f;
    border-radius: 15px;
    font-size: 16px;
}

select option {
    background-color: #2f2f2f;
    color: #ffffff;
    font-size: 16px;
}
</style>
