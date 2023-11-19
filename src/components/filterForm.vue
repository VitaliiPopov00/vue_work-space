<template>
    <aside class="filter">
        <p class="filter__link__mobile">
            Фильтр
            <svg width="8" height="6" viewBox="0 0 8 6" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M4 6L8 0H0L4 6Z" fill="#2A18FF" />
            </svg>
        </p>
        <form action="#" method="get" class="filter__form">
            <div class="filter__form__title">
                <p class="filter__form__title__text">Фильтр</p>

                <input type="reset" value="Очистить" class="filter__form__reset" />
            </div>

            <my-select
                :options="cities"
                v-model="filters.city"
            />

            <div class="filter__form__item">
                <label for="salary" class="filter__form__item__label">Заработная плата</label>
                <div class="filter__form_item__salary">
                    <input 
                        type="text" 
                        class="filter__form_item__input" 
                        name="min_salary" 
                        id="salary" 
                        placeholder="от"
                        v-model="filters.min_salary"
                        @input="validateSalary('min_salary', $event)"
                        :class="{ input_error: errors_input.min_salary}"
                    />
                    <input 
                        type="text" 
                        class="filter__form_item__input" 
                        name="max_salary" 
                        id="salary" 
                        placeholder="до" 
                        v-model="filters.max_salary"
                        @input="validateSalary('max_salary', $event)"
                        :class="{ input_error: errors_input.max_salary}"
                    />
                </div>
            </div>

            <checkbox-list
                :label="workFormat.label"
                v-model:checkboxes="workFormat.checkboxes"
            />

            <checkbox-list
                :label="experience.label"
                v-model:checkboxes="experience.checkboxes"
            />

            <checkbox-list
                :label="employment.label"
                v-model:checkboxes="employment.checkboxes"
            />

            <div class="filter__form__operation">
                <input type="submit" class="filter__form__submit btn" value="Применить" />
                <input type="reset" class="filter__form__reset no-show" value="Очистить" />
            </div>
        </form>
    </aside>
</template>

<script>
import mySelect from '@/components/UI/mySelect.vue';
import checkboxList from '@/components/UI/checkboxList.vue';

export default {
    components: {
        mySelect,
        checkboxList,
    },
    data() {
        return {
            filters: {
                city: '',
                min_salary: '',
                max_salary: '',
            },
            errors_input: {
                min_salary: false,
                max_salary: false,
            },
            cities: [],
            workFormat: {
                label: "Формат",
                checkboxes: [
                    {
                        id: 1,
                        label: "Офис",
                        name: "format_office",
                        value: false,
                    },
                    {
                        id: 2,
                        label: "Удаленный",
                        name: "format_remote",
                        value: false,
                    },
                    {
                        id: 3,
                        label: "Гибкий",
                        name: "format_flexible",
                        value: false,
                    },
                ],
            },
            experience: {
                label: "Опыт работы",
                checkboxes: [
                    {
                        id: 1,
                        label: "Не важно",
                        name: "experience_no_important",
                        value: false,
                    },
                    {
                        id: 2,
                        label: "Без опыта",
                        name: "experience_none",
                        value: false,
                    },
                    {
                        id: 3,
                        label: "От 1 года до 3-х лет",
                        name: "experience_middle",
                        value: false,
                    },
                    {
                        id: 4,
                        label: "От 3-х лет",
                        name: "experience_big",
                        value: false,
                    },
                ],
            },
            employment: {
                label: "Занятость",
                checkboxes: [
                    {
                        id: 1,
                        label: "Полная",
                        name: "employment_full",
                        value: false,
                    },
                    {
                        id: 2,
                        label: "Частичная",
                        name: "employment_middle",
                        value: false,
                    },
                    {
                        id: 3,
                        label: "Стажировка",
                        name: "employment_intership",
                        value: false,
                    },
                    {
                        id: 4,
                        label: "Проектная работа",
                        name: "employment_project",
                        value: false,
                    },
                ],
            },
            homeUrl: "https://workspace-methed.vercel.app",
        }
    },
    methods: {
        validateSalary(name, event) {
            const value = Number(event.target.value);
            this.errors_input[name] = isNaN(value) || value < 0;
        },
        async fetchCities() {
            try {
                let response = await fetch(this.homeUrl + "/api/locations");
                this.cities = await response.json();
            } catch (e) {

            }
        },
    },
    mounted() {
        this.fetchCities();
    }
}
</script>

<style>
.filter__link__mobile {
    display: none;
    color: #2A18FF;
}

.filter__link__mobile:hover {
    cursor: pointer;
}

.filter__form {
    width: 280px;
    display: flex;
    flex-direction: column;
    gap: 32px;
    font-size: 14px;
}

.filter__form__title {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.filter__form__reset {
    border: none;
    background-color: transparent;
    color: #ccc;
    font-size: 14px;
}

.filter__form__reset:hover {
    cursor: pointer;
}

.filter__form__item {
    display: flex;
    flex-direction: column;
}

.filter__form__item__label {
    margin-bottom: 12px;
}

.filter__form_item__input {
    outline: none;
    border-radius: 4px;
    border: none;
    background-color: #fff;
    height: 32px;
    padding-left: 16px;
    width: 135px;
}

.filter__form_item__input:hover {
    background-color: #F9FAFF;
}

.filter__form_item__input:focus {
    border: 1px solid #A6ADFF;
}

.filter__form_item__input::placeholder {
    color: #ccc;
    font-size: 14px;
}

.filter__form_item__salary {
    display: flex;
    gap: 10px;
}

.filter__form__item__input__section {
    display: flex;
    gap: 8px;
    align-items: center;
    margin-bottom: 8px;
}

.filter__form__item__input__section:last-child {
    margin-bottom: 0;
}

.filter__form_item__checkbox {
    height: 20px;
    width: 20px;
}

.filter__form__submit {
    border-radius: 4px;
    width: 125px;
    height: 32px;
    padding: 8px 24px;
}

.input_error {
    border: 1px solid #ff6e6e;
}

@media (max-width: 1024px) {
    .filter__link__mobile {
        display: block;
    }

    .filter__form {
        display: none;
    }
}
</style>