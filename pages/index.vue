<template>
  <div class="d-flex flex-column fill-height">
    <div>
      <FormsSearchByType :class="{ 'mt-2' : $vuetify.breakpoint.xs, 'mt-15' : $vuetify.breakpoint.smAndUp}" @pesquisar="pesquisar" />
    </div>
    <div>
      <CommonFlags class="mt-2 mb-auto" />
    </div>
    <div class="mt-auto">
      <CommonPaginationComponent :tamanho="tamanho" @pagina="paginacao" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      tamanho: 10,
      pagina: 1
    }
  },
  methods: {
    pesquisar (pesquisa) {
    },
    paginacao (pagina) {
      this.pagina = pagina
      alert(this.pagina)
    }
  }
}
</script>

<style scoped>
.search-row {
  margin-top: 118px;
}
</style>
