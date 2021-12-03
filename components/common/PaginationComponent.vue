<template>
  <div class="text-center">
    <v-pagination
      v-model="pagina"
      color="primary"
      :length="tamanho"
    />
  </div>
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
