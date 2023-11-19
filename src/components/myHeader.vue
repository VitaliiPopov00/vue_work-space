<template>
    <header>
        <div class="header_content container">
            <div class="header_content__logo">
                <svg width="17" height="16" viewBox="0 0 17 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M2 1H16V5" stroke="#171717" stroke-width="1.5" />
                    <path d="M15 13H1V9" stroke="#171717" stroke-width="1.5" />
                    <path d="M5 14.5H10.5" stroke="#171717" stroke-width="2" />
                </svg>

                <h1 class="header_content__logo__company-name">
                    <span>Work</span> Space
                </h1>
            </div>

            <a href="#work-list" class="header_content__btn btn"> Посмотреть вакансии </a>
        </div>
    </header>
</template>

<script>
export default {
    name: "my-header",

}
</script>

<style scoped>
header {
    margin-top: 40px;
    margin-bottom: 100px;
}

.header_content {
    display: flex;
    justify-content: space-between;
}

.header_content__logo {
    display: flex;
    align-items: center;
}

.header_content__logo__company-name {
    margin-left: 10px;
    font-size: 20px;
}

.header_content__logo__company-name>span {
    color: #2A18FF;
    font-weight: 600;
}

.header_content__btn {
    text-align: center;
    text-decoration: none;
    width: 285px;
    height: 48px;
    padding: 12px 32px;
    border-radius: 8px;
}

@media (max-width: 1024px) {
    .header_content__btn {
        width: 205px;
        height: 40px;
        padding: 10px 16px;
    }

    header {
        margin-top: 25px;
        margin-bottom: 60px;
    }
}

@media (max-width: 768px) {
    .header_content__btn {
        display: none;
    }

    header {
        margin-bottom: 40px;
    }
}
</style>