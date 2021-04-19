<template>
<nav class="menu" :class="{ 'menu--open' : showMenu, 'menu--close' : !showMenu}">
    <div class="menu__bg">
        <div class="menu__btns">
            <MenuHeaderContextBtn v-for="product in products" 
            :key="product.id" 
            :nameBtn="product.name" 
            :menuBtns="product.countries"
            :activeContextParent="null"/>
        </div>
    </div>
</nav>
</template>

<script>
import MenuHeaderContextBtn from './MenuHeaderContextBtn.vue'

export default {
  name: 'Menu',
  components: {
    MenuHeaderContextBtn
  },
  props: {
    showMenu: Boolean
  },
  data () {
    return {
        products: [
            {
                name: 'Апельсины',
                countries: [ 
                    {
                        name: 'Турція',
                        value: [
                            { name: 'Великі'}, 
                            { name: 'Середні'}, 
                            { name: 'Маленькі'}
                        ]
                    },
                    {
                        name: 'Іспанія',
                        value: [
                            { name: 'Великі'}, 
                            { name: 'Середні'}, 
                            { name: 'Маленькі'}
                        ]
                    }, 
                    {
                        name: 'Туніс',
                        value: [
                            { name: 'Великі'}, 
                            { name: 'Середні'}, 
                            { name: 'Маленькі'}
                        ]
                    }
                ]
            },
            {
                name: 'Яблука',
                countries: [ 
                    {
                        name: 'Украина',
                        value: [
                            { name: 'Голден'}, 
                            { name: 'Гала'}, 
                        ]
                    },
                    {
                        name: 'Іспанія',
                        value: [
                            { name: 'Голден'}, 
                            { name: 'Кальвін'}, 
                        ]
                    }
                ]
            }
            
        ]
    }
  },
  mounted () {
    this.$children[0].activeContextBtn = true
  }
}
</script>

<style lang="scss" scoped>
@keyframes open {
    from {
        margin-right: -25%;
        @media(max-width: 480px){
            margin-right: -50%;
        }
    }
    to {
        margin-right: 0;
    }
}
.menu--open{
    animation: open 0.6s;
}
</style>

<style lang="scss">
$main_text: #ffffff;

.menu{
    min-width: 25vw;
    width: max-content;
    background-repeat: no-repeat;
    background-color: rgba($color: #212120, $alpha: 0.8) ;
    background-size: 175% 100%;
    background-position: 50%;
    @media(max-width: 480px){
        width: 50%;
    }
    &__bg{
        min-width: 25vw;
        width: max-content;
        height: 100%;
        background-color: rgba($color: #212120, $alpha: 0.8) ;
        display: flex;
        flex-direction: column;
        justify-content: start;
        align-items: center;
        padding: 20px 10px;
    }
    &__header{
        display: flex;
        width: 100%;
        justify-content: space-around;
        align-items: center;
        padding: 10px 0;
        border-top: 2px solid rgba($color: #606061, $alpha: 0.9);
        border-bottom: 2px solid rgba($color: #606061, $alpha: 0.9);
        margin-bottom: 10px;
        &__img{
            height: 50px;
            width: 50px;
            border-radius: 50%;
            background-color: rgba($color: #868e96, $alpha: 0.6);
            @media (max-width: 768px){
                height: 40px;
                width: 40px;
            }
        }
        &__text{
            font-family: 'Roboto';
            font-weight: 400;
            margin: 0;
            font-size: 28px;
            color: $main_text;
            line-height: 28px;
            @media (max-width: 768px){
                font-size: 22px;
                line-height: 22px;
            }
        }
    }
    &__btns{
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        padding: 10px 5px 10px 0px;
        min-width: 25vw;
        width: max-content;
        transition: all 0.2s linear;
    }
    &--close{
        transition: all 0.4s linear;
        margin-right: -25%;
        @media(max-width: 480px){
            margin-right: -50%;
        }
        z-index: -1;
    }
}
</style>
