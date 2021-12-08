<template>
  <v-btn
    elevation="0"
    tile
    :class="{ 'borda' : $vuetify.breakpoint.smAndUp}"
    @click="backHome"
  >
    <img
      src="@/assets/svgs/icons/arrow-enter.svg"
      alt="Retornar"
    >
    <span
      v-if="!$vuetify.breakpoint.mobile"
      class="text-capitalize ml-2 primary--text"
    >Voltar</span>
  </v-btn>
</template>

<script>
export default {
  name: 'ReturnButton',
  methods: {
    backHome () {
      this.$router.push('/')
    }
  }
}
</script>

<style scoped>
.borda{
  border: 1px solid #6D2080;
}
.theme--light.v-btn.v-btn--has-bg {
  background-color: #FFF !important;
}
span.text-capitalize {
  font-size: 18px;
}
</style>
