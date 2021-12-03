<template>
  <v-btn
    width="156"
    color="primary"
    class="text-capitalize"
    @click="$emit('click')"
  >
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

<style lang="scss">
.v-btn {
  font-size: 14px;
  font-weight: 400;
  padding-block: 36px;
  border-radius: 10px;
}
</style>
