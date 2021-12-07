<template>
  <v-row>
    <v-col v-for="country in countries" :key="country.ccn3" class="d-flex child-flex" cols="12" md="4">
      <CommonFlagsFlagComponent :country="country" @details="details" />
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'Flags',
  props: {
    countries: {
      type: Array,
      required: true
    }
  },
  methods: {
    details (country) {
      this.$router.push({ name: 'Details', params: { country } })
    }
  }
}
</script>
