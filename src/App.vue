<template>
  <div id="app">
    <Header></Header>
    <Swipe></Swipe>
    <List></List>
  </div>
</template>

<script>
import Header from '@/components/Header'
import Swipe from '@/components/Swipe'
import List from '@/components/List'

export default {
  name: 'app',
  components: {
    Swipe,
    List,
    Header
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
