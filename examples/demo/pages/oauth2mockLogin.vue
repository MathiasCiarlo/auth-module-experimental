<template>
<div>
  <h2 class="text-center">Login</h2>
  <hr>
  <b-btn @click="login">Login</b-btn>
</div>
</template>

<style scoped>
.login-button {
  border: 0;
}
</style>

<script>
import busyOverlay from '~/components/busy-overlay'

export default {
  components: { busyOverlay },
  methods: {
    login() {
      const hash = this.parseQuery(this.$auth.ctx.route.hash.substr(1))
      const parsedQuery = Object.assign({}, this.$auth.ctx.route.query, hash)

      window.location.assign(`callback?code=123&state=${parsedQuery.state}`)
    },
    parseQuery(queryString) {
      const query = {}
      const pairs = queryString.split('&')
      for (let i = 0; i < pairs.length; i++) {
        const pair = pairs[i].split('=')
        query[decodeURIComponent(pair[0])] = decodeURIComponent(pair[1] || '')
      }
      return query
    }
  }
}
</script>
