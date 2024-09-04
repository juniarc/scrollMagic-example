<template>
    <main class="main-content">
        <div class="container" ref="container"> 
            <div class="item-list" ref="list">
                <Item v-for="item in dataDummy" :key="item.id" :item="item" />
            </div>
        </div>
    </main>
</template>

<script>
import { TweenMax, TimelineMax, gsap } from 'gsap';
import ScrollMagic from 'scrollmagic';
import { ScrollMagicPluginGsap } from 'scrollmagic-plugin-gsap';
import Item from './components/Item.vue';
import dataDummy from '@/data/dataDummy';

ScrollMagicPluginGsap(ScrollMagic, TweenMax, TimelineMax)

export default {
    components: {
        Item
    },
    data() {
        return {
            dataDummy
        }
    },
    mounted() {
        this.initScrollMagic()
    },
    methods: {
        initScrollMagic() {
            const controller = new ScrollMagic.Controller();

            const container = this.$refs.container
            const list = this.$refs.list

            const scrollDistance = list.clientWidth - container.clientWidth

            const slideAnimation = gsap.fromTo('.item-list', { left: '0' }, { left: -scrollDistance, ease: 'none', duration: 10 })

            new ScrollMagic.Scene({
                triggerElement: container,
                triggerHook: 0,
                duration: scrollDistance
            })
                .setPin(container)
                .setTween(slideAnimation)
                .addTo(controller)
        }
    }
}

</script>

<style scoped>
main {
    width: 100vw;
    height: 100vh;
    
}

.container {
    width: 100%;
    height: 97%;
    overflow: hidden;
    
    position: relative;
    
}

.item-list {
    width: 220vw;
    height: 100%;

    display: flex;
    align-items: flex-end;

    position: relative;
    left: 0;
    bottom: 0;
}
</style>
