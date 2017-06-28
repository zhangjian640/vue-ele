<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <ul class="tab border-1px">
      <router-link tag="li" to="/goods" class="tab-item" active-class="active">商品</router-link>
      <router-link tag="li" to="/ratings" class="tab-item" active-class="active">评论</router-link>
      <router-link tag="li" to="/seller" class="tab-item" active-class="active">商家</router-link>
    </ul>
    <keep-alive>
      <router-view :seller="seller"></router-view>
    </keep-alive>
  </div>
</template>

<script>
  import VHeader from './components/header/header'
  // import {urlParse} from 'common/js/util'
  const ERR_OK = 0
  export default {
    name: 'app',
    data () {
      return {
        seller: {
          // id: (() => {
          //   let queryParm = urlParse()
          //   console.log(queryParm)
          //   return queryParm.id
          // })()
        }
      }
    },
    components: {
      VHeader
    },
    created () {
      this.$http.get('/api/seller').then((response) => {
        if (response.data.errno === ERR_OK) {
          this.seller = response.data.data
        }
      })
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import './common/stylus/mixin.styl'
#app
  .tab
    display: flex
    width: 100%
    height: 40px
    line-height: 40px
    border-1px(rgba(7,17,27,0.1))
    .tab-item
      flex: 1
      text-align: center
      cursor: pointer
      font-size: 14px
      &.active
        color: rgb(240,20,20)
</style>