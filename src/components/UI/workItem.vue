<template>
    <div class="work-list__item" @click="$emit('showPopup', workItem.id)">
        <img 
            :src="homeUrl + workItem.logo" 
            :alt="workItem.company" 
            class="work-list__item__img"
        />
        <p class="work-list__item__company">{{ workItem.company }}</p>
        <p class="work-list__item__title">{{ workItem.title }}</p>
        <ul class="work-list__item__info">
            <li>{{ (Number(workItem.salary)).toLocaleString("ru-RU") }}₽</li>
            <li>{{ workItem.type.toLowerCase() }}</li>
            <li>{{ workItem.format.toLowerCase() }}</li>
            <li>{{ workItem.experience.toLowerCase() }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    data() {
        return {
            homeUrl: "https://workspace-methed.vercel.app/",
        }
    },
    props: {
        workItem: {
            type: Object,
            required: true,
        }
    },
}
</script>

<style scoped>
.work-list__item {
    transition: .2s;
    border-radius: 16px;
    width: 280px;
    min-height: 220px;
    background-color: #fff;
    font-size: 14px;
    display: flex;
    flex-direction: column;
    padding: 16px;
}

.work-list__item:hover {
    transition: 0s;
    background-color: #F9FAFF;
}

.work-list__item:active {
    border: 2px solid #A6ADFF;
}

.work-list__item__img {
    align-self: flex-start;
    height: 44px;
    margin-bottom: 12px;
}

.work-list__item__company {
    font-size: 20px;
    margin-bottom: 8px;
}

.work-list__item__title {
    background-color: #EAECFF;
    padding: 3px 5px;
    width: fit-content;
    border-radius: 4px;
    margin-bottom: 8px;
}

.work-list__item__info {
    list-style-type: none;
    color: #ccc;
    display: flex;
    flex-direction: column;
}

@media (max-width: 1024px) {
    .work-list__item {
        width: 220px;
    }
}

@media (max-width: 768px) {
    .work-list__item {
        width: 100%;
    }
}
</style>