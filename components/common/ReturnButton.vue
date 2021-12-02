<template>
  <v-btn
    elevation="0"
    tile
    :class="{ 'borda' : $vuetify.breakpoint.smAndUp}"
  >
    <img
      src="@/assets/svgs/icons/arrow-enter.svg"
      alt="Retornar"
    >
    <span
      v-if="!$vuetify.breakpoint.mobile"
      class="text-capitalize ml-2"
    >Voltar</span>
  </v-btn>
</template>

<style scoped>
.borda{
  border: 1px solid #6D2080;
}
.theme--light.v-btn.v-btn--has-bg {
  background-color: #FFF !important;
}
</style>
