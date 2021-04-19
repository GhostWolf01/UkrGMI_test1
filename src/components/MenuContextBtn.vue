<template>
  <div class="menu__context-btn" :class="{'menu__context-btn--open' : activeContextParent, 'menu__context-btn--close' :(!activeContextParent && activeContextParent!=null)}">
    <div class="menu__context-btn__header" @click="clickBtn" :class="{ 'menu__context-btn__header--active' : activeContextBtn}">
      <p>{{nameBtn}}</p>
      <svg v-if="menuBtns" class="context-svg" :class="{'context-svg--active' : activeContext}" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
        <path d="M24 22h-24l12-20z"/>
      </svg>
    </div>
    <MenuBtn v-for="MenuBtn in menuBtns"
    :key="MenuBtn.id"
    :nameBtn="MenuBtn.name"
    :activeContextMenu="activeContext"
    />
  </div>
</template>

<script>
import MenuBtn from './MenuBtn.vue'

export default {
  name: 'MenuContextBtn',
  props: {
    nameBtn: String,
    menuBtns: Array,
    activeContextParent: Boolean
  },
  components: {
    MenuBtn
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
          if (contxMenu.$children.length !== 0) {
            for (const menuBtn of contxMenu.$children) {
              menuBtn.activeBtn = false
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
        if (this.$children.length !== 0) {
          for (const menuBtn of this.$children) {
            menuBtn.activeBtn = false
          }
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@keyframes openContexRight {
  from {
    margin-top: -58px;
    margin-left: 0;
    margin-bottom: 0;
    opacity: 0;
    }
  to {
    margin-top: 0;
    margin-left: 310px;
    margin-bottom: 10px;
    opacity: 1;
  }
}
@keyframes openContexRightFirst {
  from {
    margin-left: 0;
    margin-bottom: 0;
    opacity: 0;
    }
  to {
    margin-left: 310px;
    margin-bottom: 10px;
    opacity: 1;
  }
}
.menu__context-btn{
  &--open{
    animation: openContexRight 0.6s;
    margin-left: 310px;
    &:nth-of-type(2){
      animation: openContexRightFirst 0.6s;
      margin-top: -58px;
    }
  }
  &--close{
    transition: all 0.4s linear;
    margin-top: -58px;
    margin-left: 0;
    margin-bottom: 0;
    opacity: 0;
    z-index: -1;
  }
}
</style>
