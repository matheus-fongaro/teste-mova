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
      <FormsAutocompleteSelect v-model="termo" :items="mockItems" :label="selectedType" :hint="descricaoDoSelect" />
    </v-col>
    <v-col v-else cols="12" md="4" />
    <v-col v-if="$vuetify.breakpoint.xs" cols="6" />
    <v-col cols="6" md="4">
      <CommonRegularButton :btn-text="'Pesquisar'" @click="$emit('pesquisar', { selectedType, termo })" />
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
          value: 'Região'
        },
        {
          text: 'Capital',
          value: 'Capital'
        },
        {
          text: 'Língua',
          value: 'Língua'
        },
        {
          text: 'País',
          value: 'País'
        },
        {
          text: 'Código de ligação',
          value: 'Código de ligação'
        }
      ],
      mockItems: [
        {
          text: 'Africa',
          value: 'Africa'
        },
        {
          text: 'Asia',
          value: 'Asia'
        },
        {
          text: 'Europe',
          value: 'Europe'
        },
        {
          text: 'North America',
          value: 'North America'
        },
        {
          text: 'Oceania',
          value: 'Oceania'
        },
        {
          text: 'South America',
          value: 'South America'
        }
      ]
    }
  },
  computed: {
    descricaoDoSelect () {
      switch (this.selectedType) {
        case 'Região':
          return 'Selecione a região'
        case 'Capital':
          return 'Selecione a capital'
        case 'Língua':
          return 'Selecione a língua'
        case 'País':
          return 'Selecione o país'
        case 'Código de ligação':
          return 'Selecione o código de ligação'
        default:
          return ''
      }
    }
  }
}
</script>
