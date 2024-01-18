<template>
    <my-header />
    <main>
        <slogan-company/>
        <div class="main_content container">
            <filter-form
                :cities = cities
                @vacancy="fetchVacancy($event)"
            />
            <work-list
                @showPopup="workItemID = $event"
                :works = works
            />
        </div>
    </main>
    <my-footer />
    <my-popup 
        @closePopup="workItemID = false"
        :workItemID="workItemID"
        v-if="workItemID"
    />
</template>

<script>
import workList from '@/components/workList.vue';
import sloganCompany from '@/components/UI/sloganCompany.vue';
import filterForm from '@/components/filterForm.vue';
import myPopup from '@/components/popup.vue';
import axios from 'axios';

export default {
    data() {
        return {
            workItemID: false,
            works: [],
            cities: [],
            homeUrl: "https://workspace-methed.vercel.app",
        }
    },
    components: {
        workList,
        sloganCompany,
        filterForm,
        myPopup,
    },
    methods: {
        async fetchVacancy(params = [])
        {
            // try {
            //     let response = await fetch(this.homeUrl + "/api/vacancy" + "?" + this.queryString(params));
            //     let data = await response.json();
            //     this.works = data.vacancies;
            // } catch (e) {
            //     console.log(e);
            // }

            try {
                let response = await axios.get(this.homeUrl + "/api/vacancy" + "?" + this.queryString(params));
                this.works = response.data.vacancies;
            } catch (e) {
                console.log(e);
            }
        },
        async fetchCities()
        {
            // try {
            //     let response = await fetch(this.homeUrl + "/api/locations");
            //     this.cities = await response.json();
            // } catch (e) {
            //     console.log(e);
            // }

            try {
                let response = await axios.get(this.homeUrl + "/api/locations");
                this.cities = response.data;
            } catch (e) {
                console.log(e);
            }
        },
        queryString(params) {
            let string = '';

            for (let name in params) {
                if ((typeof params[name]) == 'object') {
                    params[name].checkboxes.forEach(checkbox => {
                        if (checkbox.value) {
                            string += `${name}=${checkbox.name}&`;
                        }
                    })
                } else if (params[name]) {
                    string += `${name}=${params[name]}&`;
                }
            }

            return string;
        }
    },
    mounted() {
        this.fetchVacancy();
        this.fetchCities();
    }
}
</script>

<style>
/* RESET START */
* {
    margin: 0;
    padding: 0;
}

/* RESET END */

html {
    box-sizing: border-box;
    position: relative;
    font-family: 'Inter', sans-serif;
    font-size: 20px;
    color: #171717;
    background-color: #F3F4F8;
}

ul {
    list-style-type: none;
}

*,
*::after,
*::before {
    box-sizing: inherit;
}

/* MAIN START */
main {
    margin-bottom: 100px;
}

.main_content {
    display: flex;
    gap: 20px;
}
/* MAIN END */

/* ВСПОМОГАТЕЛЬНЫЕ КЛАССЫ */
.container {
    margin-inline: auto;
    width: 1180px;
}

.no-show {
    display: none;
}

.background {
    background-color: #000;
    opacity: .5;
}

.btn {
    transition: .2s;
    border: none;
    background-color: #A6ADFF;
}

.btn:hover {
    color: #fff;
    background-color: #2A18FF;
}

.btn:active {
    color: #171717;
    transition: 0s;
    border: 2px solid #4F58BE;
    background-color: #A6ADFF;
}

@media (max-width: 1440px) {
    .container {
        width: 880px;
    }

    main {
        margin-bottom: 80px;
    };
}

@media (max-width: 1024px) {
    html {
        font-size: 14px;
    }

    main {
        margin-bottom: 60px;
    }

    .container {
        width: 680px;
    }

    .main_content {
        flex-direction: column;
    }
}

@media (max-width: 768px) {
    main {
        margin-bottom: 40px;
    }

    .container {
        width: 290px;
    }
}
</style>