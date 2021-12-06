<template>
  <v-row>
    <v-col v-for="country in countries" :key="country.ccn3" class="d-flex child-flex" cols="12" md="4">
      <v-img :src="country.flags.png" max-width="316">
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
  }
}
</script>
