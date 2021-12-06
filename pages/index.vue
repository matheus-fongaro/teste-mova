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
    const data = await this.$axios.$get('https://restcountries.com/v3.1/all')
    this.countries = data
    data.length > 1 ? this.tamanho = Math.ceil(data.length / 12) : this.tamanho = 1
  },
  methods: {
    async pesquisar (pesquisa) {
      // as duas versões da api tem variáveis com nomes diferentes, e a versão 3.1 não tem o calling code do
      // jeito que preciso, então por isso precisei usar as duas versões, dependendo da requisição
      const version = pesquisa.selectedType === 'callingcode' ? 'v2' : 'v3.1'
      const data = await this.$axios.$get(`https://restcountries.com/${version}/${pesquisa.selectedType}/${pesquisa.termo}`)
      this.pagina = 1
      data.length > 1 ? this.tamanho = Math.ceil(data.length / 12) : this.tamanho = 1
      this.countries = data
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
