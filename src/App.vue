<template>
  <div id="app">
    <myHeader></myHeader>
    <myNav></myNav>
    <router-view/>
  </div>
</template>

<script>
import myHeader from './components/header/header'
import myNav from './components/nav/nav'

export default {
  name: 'App',
  components: {
    myHeader,
    myNav,
  }
}
</script>

<style>

</style>
