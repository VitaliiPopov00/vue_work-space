<template>
    <div class="filter__form__item">
        <label for="city_list" class="filter__form__item__label">Город</label>
        <select 
            name="city" 
            id="city_list" 
            class="filter__form_item__input"
            :value="modelValue"
            @change="$emit('update:modelValue', $event.target.value)"
        >
            <option value="">Выбрать город</option>
            <option 
                v-for="option, index in options" 
                :value="option"
                :key="index"
            >{{ option }}</option>
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
                required: true,
            }
        },
    }
</script>

<style scoped>
.filter__form_item__input {
    width: 100%;
}
</style>