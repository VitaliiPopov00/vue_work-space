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
    components: {
        workItem,
    },
    data() {
        return {
            works: [],
            homeUrl: "https://workspace-methed.vercel.app",
        }
    },
    methods: {
        async fetchVacancy()
        {
            try {
                let response = await fetch(this.homeUrl + "/api/vacancy");
                let data = await response.json();
                this.works = data.vacancies;
            } catch (e) {

            }
        },
    },
    mounted() {
        this.fetchVacancy();
    }
}
</script>

<style scoped>
.work-list {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

@media (max-width: 1024px) {
    .work-list {
        gap: 10px;
    }
}
</style>