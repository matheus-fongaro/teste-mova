<template>
  <div class="d-flex flex-column fill-height">
    <div>
      <FormsSearchByType :class="{ 'mt-2' : $vuetify.breakpoint.xs, 'mt-15' : $vuetify.breakpoint.smAndUp}" @pesquisar="pesquisar" />
    </div>
    <div>
      <CommonFlags class="mt-2 mb-auto" :countries="paginatedCountries" />
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
      tamanho: 1,
      pagina: 1,
      countries: []
    }
  },
  computed: {
    paginatedCountries () {
      return this.countries.slice((this.pagina - 1) * 12, this.pagina * 12)
    }
  },
  async mounted () {
    const data = await this.$axios.$get('https://restcountries.com/v2/all')
    this.countries = data
    this.tamanho = Math.ceil(data.length / 12)
  },
  methods: {
    pesquisar (pesquisa) {
    },
    paginacao (pagina) {
      this.pagina = pagina
    }
  }
}
</script>

<style scoped>
.search-row {
  margin-top: 118px;
}
</style>
