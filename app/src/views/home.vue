<template>
  <div class="container home-view">
    <div class="information-box" v-show="showInfo">
      <navigator :token="token"></navigator>
      <informationsContainer :infomation="user" @infoHandler="infoHandler"></informationsContainer>
    </div>
    <navigatorColumn v-show="!showInfo" @navColumnHandler="navColumnHandler"></navigatorcolumn>
    <div v-bind:class="{'content-layout': showInfo, 'content-bar-layout': !showInfo}">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
import navigator from '../components/navigator'
import navigatorColumn from '../components/navigator-column'
import informationsContainer from '../components/information-container'
import articleCard from '../components/article-card'

import { mapGetters, mapActions } from 'vuex'

export default {
  computed: {
    ...mapGetters(['user', 'post', 'token'])
  },
  methods: {
    ...mapActions(['queryResource']),
    infoHandler () {
      this.showInfo = !this.showInfo
    },
    navColumnHandler () {
      this.showInfo = !this.showInfo
    }
  },
  created () {
    if (this.token) {
      this.queryResource({ url: 'post', args: {} }).then(body => {
      })
    } else {
      this.$router.push('/auth')
    }
  },
  components: {
    navigator,
    informationsContainer,
    navigatorColumn,
    articleCard
  },
  data () {
    return {
      showInfo: true
    }
  }
}

</script>

<style>
@import '../assets/styles/home.scss';
</style>
