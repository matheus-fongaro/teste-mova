<template>
  <div class="d-flex flex-column fill-height">
    <div>
      <FormsSearchByType :class="{ 'mt-2' : $vuetify.breakpoint.xs, 'mt-15' : $vuetify.breakpoint.smAndUp}" @pesquisar="pesquisar" />
    </div>
    <div>
      <CommonFlags class="mt-2 mb-auto" :countries="paginatedCountries" :max-width="'316'" />
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
      if (this.countries.length) {
        return this.countries.slice((this.pagina - 1) * 12, this.pagina * 12)
      } else {
        return this.countries
      }
    }
  },
  async mounted () {
    const data = await this.$axios.$get('https://restcountries.com/v2/all')
    this.countries = data
    data.length > 1 ? this.tamanho = Math.ceil(data.length / 12) : this.tamanho = 1
  },
  methods: {
    async pesquisar (pesquisa) {
      const data = await this.$axios.$get(`https://restcountries.com/v2/${pesquisa.selectedType}/${pesquisa.termo}`)
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
