<template>
    <section class="work-list" id="work-list">
        <work-item 
            v-for="work in works" 
            :key="work.id" 
            :workItem="work"
            @showPopup="$emit('showPopup', $event)"
        />
    </section>
</template>

<script>
import workItem from '@/components/UI/workItem.vue';

export default {
    props: {
        works: {
            type: Array,
            required: true,
        }
    },
    components: {
        workItem,
    },
}
</script>

<style scoped>
.work-list {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    align-self: flex-start;
}

@media (max-width: 1024px) {
    .work-list {
        gap: 10px;
    }
}
</style>