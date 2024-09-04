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
            dataDummy,
            controller: null,
            scene: null,
            screenWidth: window.innerWidth
        }
    },
    watch: {
        screenWidth(newWidth) {
            this.updateScrollMagic(newWidth)
        }
    },
    mounted() {
        this.updateScrollMagic()
        window.addEventListener('resize', this.handleResize)
    },
    beforeUnmount() {
        window.removeEventListener('resize', this.handleResize)
        this.destroyScrollMagic()
    },
    methods: {
        initScrollMagic() {
            const container = this.$refs.container
            const list = this.$refs.list

            if(this.controller) {
                this.destroyScrollMagic();
            }

            this.controller = new ScrollMagic.Controller();
            const scrollDistance = list.clientWidth - container.clientWidth

            const slideAnimation = gsap.fromTo('.item-list', { left: '0' }, { left: -scrollDistance, ease: 'none', duration: 10 })

            this.scene = new ScrollMagic.Scene({
                triggerElement: container,
                triggerHook: 0,
                duration: scrollDistance
            })
                .setPin(container)
                .setTween(slideAnimation)
                .addTo(controller)
        },
        handleResize() {
            this.screenWidth = window.innerWidth;
        },
        updateScrollMagic(width) {
            if(width <= 375) {
                this.destroyScrollMagic();
            } else {
                this.initScrollMagic();
            }
        },
        destroyScrollMagic() {
            if (this.scene) {
                this.scene.destroy(true);
                this.scene = null;
            }
            if (this.controller) {
                this.controller.destroy(true);
                this.controller = null;
            }
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

@media screen and (max-width: 768px) {
    .item-list {
        width: 260vw;
    }
}

@media screen and (max-width: 375px) {
    .container {
        overflow: visible;
    }
    .item-list {
        width: 100%;
        height: 100%;

        flex-direction: column;
        align-items: center;

        padding: 20px;
    }
}
</style>
