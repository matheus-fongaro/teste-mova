<template>
  <v-app>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      color="white"
      height="100px"
      app
    >
      <LogoMovaLogo @click="goBack" />
      <v-spacer />
      <CommonReturnButton @click="goBack" />
    </v-app-bar>
    <v-main>
      <v-container class="tela-cheia">
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>Matheus Fongaro &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Mova'
    }
  },
  methods: {
    goBack () {
      this.$router.push('/')
    }
  }
}
</script>

<style>
.tela-cheia {
  height: 100%;
}
</style>
