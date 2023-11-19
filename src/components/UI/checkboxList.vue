<template>
    <div class="filter__form__item">
        <label for="" class="filter__form__item__label">{{ label }}</label>
        <div 
            class="filter__form__item__input__section"
            v-for="checkbox in checkboxes"
            :key="checkbox.id"
        >
            <input 
                type="checkbox" 
                class="filter__form_item__checkbox" 
                :name="checkbox.name" 
                :id="checkbox.name"
                v-model="checkbox.value"
                @change="$emit('update:checkboxes', JSON.parse(JSON.stringify(checkboxes)))"
            />
            <label
                :for="checkbox.name"
            >{{ checkbox.label }}</label>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        label: {
            type: String,
            required: true,
        },
        checkboxes: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style scoped>
</style>