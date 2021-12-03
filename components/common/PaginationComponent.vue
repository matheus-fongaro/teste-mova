<template>
  <v-pagination
    v-model="pagina"
    color="primary"
    :length="tamanho"
  />
</template>

<script>
export default {
  name: 'PaginationComponent',
  props: {
    tamanho: {
      type: Number,
      required: true
    }
  },
  data () {
    return {
      pagina: 1
    }
  },
  watch: {
    pagina (val) {
      this.$emit('pagina', val)
    }
  }
}
</script>
