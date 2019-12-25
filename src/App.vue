<template>
  <div id="app">
    <transition name="fade" mode="out-in">
      <Start @sendCode="reciveCode" v-if="show === 'start'"/>
      <Tree @home="show = 'start'" :code="code" v-else/>
    </transition>
  </div>
</template>

<script>
import Start from './components/Start.vue'
import Tree from './components/Tree.vue'

export default {
  name: 'app',
  components: {
    Start,
    Tree
  },
  data () {
    return {
      show: 'start',
      code: ''
    }
  },
  methods: {
    reciveCode (code) {
      this.code = code.replace(/\s/g, '')
      this.show = 'tree'
    }
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}

html, body, #app {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
