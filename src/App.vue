<template>
  <div id="app">
    <myHeader :poiInfo='poiInfo'></myHeader>
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
  },
  data () {
    return {
      poiInfo: {},
    }
  },
  created () {
    let vm = this
    this.$axios.get('/api/goods')
        .then(function(res){
          let dataSource = res.data
          if(dataSource.code == 0){
            vm.poiInfo = dataSource.data.poi_info
          }
        })
        .catch(function(err){
          console.log(err)
        })
  }
}
</script>

<style>

</style>
