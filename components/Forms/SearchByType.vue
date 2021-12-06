<template>
  <v-row
    align="start"
  >
    <v-col cols="12" md="4">
      <FormsRegularSelect
        v-model="selectedType"
        :items="items"
        :label="'Filtrar por:'"
      />
    </v-col>
    <v-col v-if="selectedType !== ''" cols="12" md="4">
      <FormsAutocompleteSelect v-model="termo" :items="autocompleteItems" :label="selectedType" :hint="descricaoDoSelect" />
    </v-col>
    <v-col v-else cols="12" md="4" />
    <v-col v-if="$vuetify.breakpoint.xs" cols="6" />
    <v-col cols="6" md="4">
      <CommonRegularButton :is-disabled="isDisabled" :btn-text="'Pesquisar'" @click="$emit('pesquisar', { selectedType, termo })" />
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'SearchByType',
  data () {
    return {
      selectedType: '',
      termo: '',
      items: [
        {
          text: 'Região',
          value: 'region'
        },
        {
          text: 'Capital',
          value: 'capital'
        },
        {
          text: 'Língua',
          value: 'lang'
        },
        {
          text: 'País',
          value: 'name'
        },
        {
          text: 'Código de ligação',
          value: 'callingcode'
        }
      ],
      autocompleteItems: []
    }
  },
  computed: {
    descricaoDoSelect () {
      switch (this.selectedType) {
        case 'region':
          return 'Selecione a região'
        case 'capital':
          return 'Selecione a capital'
        case 'lang':
          return 'Selecione a língua'
        case 'name':
          return 'Selecione o país'
        case 'callingcode':
          return 'Selecione o código de ligação'
        default:
          return ''
      }
    },
    isDisabled () {
      return this.termo === ''
    }
  },
  watch: {
    selectedType (newValue) {
      this.termo = ''
      this.autocompleteItems = []
      switch (newValue) {
        case 'region':
          this.autocompleteItems = this.regionItems()
          break
        case 'capital':
          this.autocompleteItems = this.capitalItems()
          break
        case 'lang':
          this.autocompleteItems = this.languageItems()
          break
        case 'name':
          this.autocompleteItems = this.countryItems()
          break
        case 'callingcode':
          this.autocompleteItems = this.callingCodeItems()
          break
        default:
          this.autocompleteItems = []
      }
    }
  },
  methods: {
    async regionItems () {
      const dados = await this.$axios.$get('https://restcountries.com/v3.1/all?fields=region')

      this.autocompleteItems = dados.map((item) => {
        return {
          text: item.region,
          value: item.region
        }
      })
    },
    async capitalItems () {
      const dados = await this.$axios.$get('https://restcountries.com/v3.1/all?fields=capital')

      this.autocompleteItems = dados.map((item) => {
        return {
          text: item.capital[0],
          value: item.capital[0]
        }
      })
    },
    async languageItems () {
      const dados = await this.$axios.$get('https://restcountries.com/v3.1/all?fields=languages')

      const flattened = {}

      dados.forEach((obj) => {
        Object.keys(obj.languages).forEach((key) => {
          flattened[key] = obj.languages[key]
        })
      })

      this.autocompleteItems = Object.keys(flattened).map((key) => {
        return {
          text: flattened[key],
          value: flattened[key]
        }
      })
    },
    async countryItems () {
      const dados = await this.$axios.$get('https://restcountries.com/v3.1/all?fields=name')

      this.autocompleteItems = dados.map((item) => {
        return {
          text: item.name.common,
          value: item.name.common
        }
      })
    },
    async callingCodeItems () {
      const dados = await this.$axios.$get('https://restcountries.com/v2/all?fields=callingCodes')

      this.autocompleteItems = dados.map((item) => {
        return {
          text: item.callingCodes[0],
          value: item.callingCodes[0]
        }
      })
    }
  }
}
</script>
