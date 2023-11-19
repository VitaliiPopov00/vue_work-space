<template>
    <section class="popup" v-if="workItem">
        <div :style="computedStyles">
            <div class="popup__title">
                <img 
                    :src="homeUrl + workItem.logo" 
                    alt="img" 
                    class="popup__title__img" />
                <div class="popup__title__info">
                    <p>{{ workItem.company }}</p>
                    <span>{{ workItem.title }}</span>
                </div>
            </div>
            <div class="popup__body">
                <div class="popup__info">
                    <p v-html="formattedDescription" />
                </div>
                <ul class="popup__tags">
                    <li class="popup__tags__item">от {{ (Number(workItem.salary)).toLocaleString('ru-RU') }}₽</li>
                    <li class="popup__tags__item">{{ workItem.type }}</li>
                    <li class="popup__tags__item">{{ workItem.format }}</li>
                    <li class="popup__tags__item">{{ workItem.experience }}</li>
                    <li class="popup__tags__item">{{ workItem.location }}</li>
                </ul>
            </div>
            <div class="popup__link">
                Отправляйте резюме на
                <a href="mailto:CreativePeople@gmail.com">{{ workItem.email }}</a>
            </div>
            <img src="img/site/likemen.png" alt="likeman" class="popup__likeman">
            <img 
                src="img/site/close.svg" 
                alt="close" 
                class="popup__close"
                @click="$emit('closePopup')">
        </div>
    </section>
</template>

<script>
    export default {
        data() {
            return {
                homeUrl: "https://workspace-methed.vercel.app/",
                workItem: false
            }
        },
        props: {
            workItemID: {
                type: String,
                required: true,
            }
        },
        computed: {
            formattedDescription() {
                return this.workItem.description.replace(/\n/g, "<br>");
            },
            computedStyles() {
                const offsetY = window.pageYOffset;

                return {
                    marginTop: offsetY + 150 + 'px',
                    marginInline: 'auto'
                };
            },
        },
        async mounted() {
            try {
                let response = await fetch(this.homeUrl + "api/vacancy/" + this.workItemID);
                this.workItem = await response.json();
            } catch (e) {

            }
        }
    }
</script>

<style scoped>
    .popup {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.5);
    }

    .popup > div {
        width: 780px;
        background-color: #fff;
        padding: 36px;
        border-radius: 16px;
        font-size: 14px;
        position: relative;
    }

    .popup__title {
        display: flex;
        align-items: center;
        gap: 20px;
        margin-bottom: 32px;
        flex-wrap: wrap;
    }

    .popup__title__info {
        display: flex;
        flex-direction: column;
        gap: 12px;
        font-size: 32px;
    }

    .popup__title__info > span {
        font-size: 20px;
        padding: 5px 10px;
        background-color: #EAECFF;
        align-self: flex-start;
        border-radius: 4px;
    }

    .popup__title__img {
        height: 60px;
    }

    .popup__body {
        display: flex;
        gap: 20px;
        margin-bottom: 32px;
    }
    
    .popup__info {
        width: 465px;
    }

    .popup__tags {
        display: flex;
        flex-direction: column;
        gap: 4px;
    }

    .popup__tags__item {
        padding: 3px 10px;
        border-radius: 30px;
        background-color: #EAECFF;
        width: fit-content;
    }

    .popup__link {
        margin-bottom: 44px;
    }

    .popup__link > a {
        text-decoration: none;
    }

    .popup__likeman {
        position: absolute;
        right: 0;
        bottom: 0;
    }

    .popup__close {
        position: absolute;
        top: 16px;
        right: 16px;
    }

    .popup__close:hover {
        cursor: pointer;
    }

    @media (max-width: 1024px) {
        .popup > div {
            width: 680px;
        }
    }

    @media (max-width: 768px) {
        .popup > div {
            width: 290px;
            padding: 24px 15px 24px 15px;
        }
        .popup__title {
            margin-bottom: 24px;
        }

        .popup__title__info {
            font-size: 20px;
        }

        .popup__title__info > span {
            font-size: 12px;
            padding: 5px 10px;
            background-color: #EAECFF;
            align-self: flex-start;
        }

        .popup__body {
            flex-direction: column;
            gap: 24px;
            margin-bottom: 24px;
        }

        .popup__info {
            width: 260px;
        }

        .popup__link > a {
            display: block;
        }

        .popup__link {
            margin-bottom: 0px;
        }

        .popup__likeman {
            display: none;
        }
    }
</style>