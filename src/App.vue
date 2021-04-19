<template>
  <div id="app">
    <Menu :showMenu="true"/>
    <div class="activeComponent">
      <p>{{activeComponent}}</p>
    </div>
  </div>
</template>

<script>
import Menu from './components/Menu.vue'

export default {
  name: 'App',
  components: {
    Menu
  },
  data() {
    return {
      activeComponent: ''
    }
  },
  mounted() {
    this.$root.$on('clickBtn',  (text) => {
      this.activeComponent = text
    })
  }
}
</script>

<style lang="scss">

html, body {
  scrollbar-color: rgba(#66615b, 0.8) rgba(#ffffff, 0);
}
::-webkit-scrollbar{
  background-color: rgba(#ffffff, 0);
  width: 5px;
  height: 5px;
}
::-webkit-scrollbar-thumb{
  border-radius: 5px;
  background-color: rgba(#66615b, 0.8);
}

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scrollbar-width: thin;
}
#app{
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.activeComponent {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    margin-left: 50px;
    min-width: 200px;
    width: auto;
    height: 100px;
    font-family: 'Roboto';
    font-weight: 400;
    font-size: 28px;
    color: black;
    line-height: 28px;
    text-align: center;
}

</style>
