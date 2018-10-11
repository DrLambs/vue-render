<template>
  <div id="app">
    <RenderTest msg="Render Test" :level="3" :items="items">
      <div class="header">default header</div>
      <p slot="header">slot header</p>
    </RenderTest>
  </div>
</template>

<script>
import RenderTest from './components/RenderTest.vue'

export default {
  name: 'app',
  components: {
    RenderTest
  },
  data() {
    return {
      items: [
        {
          name: 'hello'
        },
        {
          name: 'vue'
        },
        {
          name: 'js'
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
