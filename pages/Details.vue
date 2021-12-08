<template>
  <div>
    <v-row class="mt-lg-12">
      <v-col
        cols="12"
        md="5"
      >
        <CommonFlagsFlagComponent
          :country="country"
          :max-width="'443'"
          :max-height="'256'"
        />
      </v-col>
      <v-col
        cols="12"
        md="4"
      >
        <p>Nome: {{ country.translations.br }}</p>
        <p>Capital: {{ country.capital }}</p>
        <p>Região: {{ country.region }}</p>
        <p>Sub-região: {{ country.subregion }}</p>
        <p>População: {{ country.population }}</p>
        <div
          v-for="lingua of country.languages"
          :key="lingua.nome"
        >
          <p>Línguas: {{ lingua.name }}</p>
        </div>
      </v-col>
    </v-row>
    <div v-if="hasBorderCountries">
      <p class="mt-lg-15">
        Países Vizinhos:
      </p>
      <v-row>
        <v-col
          v-for="paisVizinho of paginatedBorderCountries"
          :key="paisVizinho.alpha3Code"
          cols="12"
          md="4"
        >
          <CommonFlagsFlagComponent
            :country="paisVizinho"
            :max-width="'316'"
            :max-height="'181'"
            @details="changeCountry"
          />
        </v-col>
      </v-row>
      <CommonPaginationComponent
        :tamanho="tamanho"
        @pagina="paginacao"
      />
    </div>
    <div
      v-else
      class="mt-lg-15"
    >
      <strong>Este país não faz fronteira com nenhum outro.</strong>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Details',
  data () {
    return {
      country: {},
      borderCountriesArray: [],
      borderCountries: [],
      hasBorderCountries: false,
      tamanho: 1,
      pagina: 1
    }
  },
  computed: {
    paginatedBorderCountries () {
      if (this.borderCountries.length) {
        return this.borderCountries.slice((this.pagina - 1) * 12, this.pagina * 12)
      } else {
        return this.borderCountries
      }
    }
  },
  created () {
    this.country = this.$route.params.country
  },
  async mounted () {
    if (this.country.borders) {
      this.borderCountriesArray = Object.values(this.$route.params.country.borders).join(',')
      this.borderCountries = await this.$axios.$get(`https://restcountries.com/v2/alpha?codes=${this.borderCountriesArray}`)
      this.borderCountries.length > 1 ? this.tamanho = Math.ceil(this.borderCountries.length / 12) : this.tamanho = 1
      this.hasBorderCountries = true
    } else {
      this.hasBorderCountries = false
    }
  },
  methods: {
    async changeCountry (country) {
      this.country = country
      if (this.country.borders) {
        this.borderCountriesArray = Object.values(this.country.borders).join(',')
        this.borderCountries = await this.$axios.$get(`https://restcountries.com/v2/alpha?codes=${this.borderCountriesArray}`)
        this.hasBorderCountries = true
      } else {
        this.hasBorderCountries = false
      }
    },
    paginacao (pagina) {
      this.pagina = pagina
    }
  }
}
</script>

<style>
p,
strong {
  font-size: 18px;
}
</style>
