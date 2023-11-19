<template>
    <footer>
        <div class="footer_content container">
            <div class="footer_content__info-company">
                <div class="footer_content__info-company__logo">
                    <svg width="17" height="16" viewBox="0 0 17 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M2 1H16V5" stroke="#171717" stroke-width="1.5" />
                        <path d="M15 13H1V9" stroke="#171717" stroke-width="1.5" />
                        <path d="M5 14.5H10.5" stroke="#171717" stroke-width="2" />
                    </svg>

                    <h1 class="footer_content__info-company__logo__text">
                        <span>Work</span> Space
                    </h1>
                </div>

                <p class="footer_content__info-company__copyright">
                    © Work Space, 2023
                </p>
            </div>

            <p class="footer_content__dev-info">
                Designer: Anastasia Ilina<br>
                Developer: Vitalii Popov
            </p>
        </div>
    </footer>
</template>

<script>
export default {
    name: "my-footer",

}
</script>

<style scoped>
footer {
    font-size: 14px;
    margin-bottom: 24px;
}

.footer_content {
    display: flex;
    justify-content: space-between;
}

.footer_content__info-company__logo__text {
    font-size: 20px;
    margin-left: 10px;
}

.footer_content__info-company__logo {
    display: flex;
    align-items: center;
    margin-bottom: 27px;
}

.footer_content__info-company__logo__text>span {
    color: #A6ADFF;
}

.footer_content__info-company__copyright {
    margin-bottom: 22px;
}

.footer_content__dev-info {
    align-self: flex-end;
    line-height: 2;
}

@media (max-width: 768px) {
    .footer_content {
        flex-direction: column;
    }

    .footer_content__info-company__logo {
        margin-bottom: 16px;
    }

    .footer_content__info-company__copyright {
        margin-bottom: 30px;
    }

    .footer_content__dev-info {
        align-self: flex-start;
        line-height: 2;
    }
}
</style>