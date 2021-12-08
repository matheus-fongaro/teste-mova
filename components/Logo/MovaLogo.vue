<template>
  <img
    alt="Mova Logo"
    src="@/assets/svgs/logo/logo_principal.svg"
    @click="goBack"
  >
</template>

<script>
export default {
  name: 'MovaLogo',
  methods: {
    goBack () {
      this.$router.push('/')
    }
  }
}
</script>

<style>
img:hover {
  cursor: pointer;
}
</style>
