<template>
  <div>
    <FormsSearchByType :class="{ 'mt-2' : $vuetify.breakpoint.xs, 'mt-15' : $vuetify.breakpoint.smAndUp}" @pesquisar="pesquisar" />
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data () {
    return {
    }
  },
  methods: {
    pesquisar (pesquisa) {
    }
  }
}
</script>

<style scoped>
.search-row {
  margin-top: 118px;
}
</style>
