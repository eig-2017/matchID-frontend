<template>
  <div id="app">
    <header>
      <match-id-navigation></match-id-navigation>
    </header>

    <router-view></router-view>
  </div>
</template>

<script>
import matchIdNavigation from './components/Navigation'
import Vue from 'vue'
import VueCodeMirror from 'vue-codemirror'
import VueClipboard from 'vue-clipboard2'

import apiConf from './assets/json/backend.json'
import localization from './assets/json/lang.json'

import lodash from 'lodash'

Vue.prototype.$lodash = lodash

Vue.use(VueCodeMirror)
Vue.use(VueClipboard)

window.bus = new Vue()

Vue.mixin({
  data () {
    return {
      apiUrl: apiConf.api.url,
      localization: localization,
      lang: localization.default
    }
  },
  mounted () {
    window.bus.$on('langChange', value => {
      this.lang = value
    })
  }
})

export default {
  name: 'app',
  components: {
    matchIdNavigation
  }
}
</script>

<style lang="scss" src="./assets/scss/style.scss"></style>
