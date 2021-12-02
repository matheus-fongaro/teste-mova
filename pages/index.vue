<template>
  <v-row
    justify="space-around"
    align="start"
    class="search-row"
    no-gutters
  >
    <v-col md="3">
      <div>
        <div class="mb-0 ml-1 primary--text">
          Filtrar por:
        </div>
        <v-select
          v-model="filtroSelecionado"
          class="mt-0"
          :items="tiposDeFiltro"
          label="Escolha uma opção"
        />
      </div>
    </v-col>
    <v-col md="3">
      <p v-if="filtroSelecionado != null">
        Outra coisa
      </p>
    </v-col>
    <v-col md="3">
      <CommonRegularButton :btn-text="'Pesquisar'" />
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
      tiposDeFiltro: [
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
          value: 'country'
        },
        {
          text: 'Código de ligação',
          value: 'code'
        }
      ],
      filtroSelecionado: null
    }
  }
}
</script>

<style scoped>
.search-row {
  margin-top: 218px;
}
</style>
