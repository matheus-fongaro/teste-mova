<template>
  <v-btn color="primary" class="px-3 text-capitalize">
    {{ btnText }}
  </v-btn>
</template>

<script>
export default {
  name: 'RegularButton',
  props: {
    btnText: {
      type: String,
      default: 'Ok'
    }
  }
}
</script>

<style scoped>
.v-btn {
  font-size: 14px;
  font-weight: 400;
}
</style>
