<template>
  <div class="menu__context-btn">
    <div class="menu__context-btn__header" @click="clickBtn" :class="{ 'menu__context-btn__header--active' : activeContextBtn}">
      <p>{{nameBtn}}</p>
      <svg v-if="menuBtns" class="context-svg" :class="{'context-svg--active' : activeContext}" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
        <path d="M24 22h-24l12-20z"/>
      </svg>
    </div>
    <MenuContextBtn
    v-for="MenuBtn in menuBtns"
    :key="MenuBtn.id"
    :nameBtn="MenuBtn.name"
    :menuBtns="MenuBtn.value"
    :activeContextParent="activeContext"
    />
  </div>
</template>

<script>
import MenuContextBtn from './MenuContextBtn.vue'

export default {
  name: 'MenuHeaderContextBtn',
  props: {
    nameBtn: String,
    menuBtns: Array,
  },
  components: {
    MenuContextBtn
  },
  data () {
    return {
      activeBtn: false,
      activeContext: false,
      activeContextBtn: false
    }
  },
  methods: {
    clickBtn () {
      if (this.activeBtn === false) {
        for (const contxMenu of this.$parent.$children) {
          if (contxMenu.$children.length != 0) {
            for (const menuBtn of contxMenu.$children) {
              if(menuBtn.$children.length != 0) {
                for (const mBtn of menuBtn.$children) {
                  mBtn.activeBtn = false
                }
              }
              menuBtn.activeBtn = false
              menuBtn.activeContext= false
              menuBtn.activeContextBtn= false
            }
          }
          contxMenu.activeBtn = false
          contxMenu.activeContext = false
          contxMenu.activeContextBtn = false
        }
        this.activeBtn = true
        this.activeContext = true
        this.activeContextBtn = true
      } else {
        this.activeContext = false
        this.activeBtn = false
        if (this.$children.length != 0) {
          for (const menuBtn of this.$children) {
              if(menuBtn.$children.length != 0) {
                for (const mBtn of menuBtn.$children) {
                  mBtn.activeBtn = false
                }
              }
              menuBtn.activeBtn = false
              menuBtn.activeContext= false
              menuBtn.activeContextBtn= false
          }
        }
      }
    }
  }
}
</script>

<style lang="scss">
$main_text: #808080;
$hover_text: #ffffff;
$active_text: #ffffffc0;

.menu__context-btn{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  cursor: pointer;
  width: max-content;
  min-width: 300px;
  &__header{
    width: 100%;
    max-width: 300px;
    height: 48px;
    margin-bottom: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 10px;
    padding-left: 10px;
    font-family: 'Roboto';
    font-weight: 400;
    font-size: 28px;
    color: $main_text;
    line-height: 28px;
    transition: all 0.15s linear;
    @media(max-width: 768px)
    {
      font-size: 20px;
      line-height: 20px;
    }
    & p{
      width: 100%;
    }
    &:hover{
      background-color: rgba($color: #c8c8c8, $alpha: 0.2);
      color: $hover_text;
    }
    &--active{
      background-color: rgba($color: #28a745, $alpha: 0.7);
      color: $active_text;
      &:hover {
        background-color: rgba($color: #28a745, $alpha: 0.8);
        color: $hover_text;
      }
    }
  }
}
.context-svg{
  width: 15px;
  height: 15px;
  margin-right: 10px;
  transition: all 0.25s ease-in-out;
  filter: invert(100%);
  &--active{
    transform: rotate(180deg);
  }
}
</style>
