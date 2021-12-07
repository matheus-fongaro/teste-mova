<template>
  <v-img :src="country.flag" :width="maxWidth" alt="Bandeira do país" @click="details(country)">
    <template #placeholder>
      <v-row
        class="fill-height ma-0"
        align="center"
        justify="center"
      >
        <v-progress-circular
          indeterminate
          color="grey lighten-5"
        />
      </v-row>
    </template>
  </v-img>
</template>

<script>
export default {
  name: 'FlagComponent',
  props: {
    country: {
      type: Object,
      required: true
    },
    maxWidth: {
      type: String,
      default: '100px'
    }
  },
  data () {
    return {
      borderCountries: []
    }
  },
  methods: {
    details (country) {
      this.$emit('details', country)
    }
  }
}
</script>
