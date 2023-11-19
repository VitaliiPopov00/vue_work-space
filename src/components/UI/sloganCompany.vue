<template>
    <section class="slogan container">
        <h1 class="slogan__text">
            Найди работу<br />
            <span>Своей мечты</span>
        </h1>

        <img src="img/site/slogan_img.png" alt="img" class="slogan__img" />
    </section>
</template>

<script>
export default {

}
</script>

<style scoped>
.slogan {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 100px;
}

.slogan__text {
    text-transform: uppercase;
    font-size: 90px;
    line-height: 108px;
}

.slogan__text>span {
    color: #2A18FF;
}

@media (max-width: 1440px) {
    .slogan__text {
        font-size: 64px;
        line-height: 76px;
    }

    .slogan {
        margin-bottom: 80px;
    }

    img {
        width: 340px;
    }
}

@media (max-width: 1024px) {
    .slogan__text {
        font-size: 50px;
        line-height: 62px;
    }
    
    .slogan {
        margin-bottom: 60px;
    }

    img {
        width: 269px;
    }
}

@media (max-width: 768px) {
    .slogan__text {
        font-size: 32px;
        line-height: 38px;
    }

    .slogan {
        flex-direction: column;
        margin-bottom: 40px;
    }
}
</style>