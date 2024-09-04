<script setup>
const props = defineProps({
    item: {
        type: Object,
        required: true
    }
})
</script>

<template>
    <div class="item__wrapper">
        <div class="item-img__wrapper">
            <img :src="item.image" :alt="item.title" class="item-img">
        </div>
        <div class="content__wrapper">
            <div class="content-text__wrapper">
                <h1 class="content-title">{{ item.title }}</h1>
                <p class="content-desc">{{ item.description }}</p>
            </div>
            <div class="text-bg-color"></div>
        </div>
    </div>
</template>

<style scoped>
.item__wrapper {
    width: 25vw;
    height: 30rem;
    background-color: white;
    border-radius: 16px;

    box-shadow: 0px 5px 30px 6px rgba(0, 0, 0, 0.05);
    float: left;

    margin: 1rem;

    position: relative;
    bottom: 0;

    transition: all .5s ease;

    cursor: pointer;
}

.item__wrapper:hover {
    bottom: 5%;
}

.item-img__wrapper {
    width: 100%;
    height: 55%;
    min-height: 55%;
}

.item-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;

    border-radius: 16px 16px 0 0;
}

.content__wrapper {
    padding: 40px;

    position: relative;
}

.content-text__wrapper {
    z-index: 1;
    position: relative;
}

.content-title {
    margin-bottom: 16px;

    height: 5rem;
}

.text-bg-color {
    position: absolute;
    bottom: -2%;
    left: 0;

    z-index: 0;

    background-color: #f5f5f5;
    width: 100%;
    height: 0;

    border-radius: 0 0 1rem 1rem;

    transition: all .5s ease;
}

.item__wrapper:hover .text-bg-color {
    height: 102%;
}

</style>