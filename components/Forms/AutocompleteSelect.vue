<template>
  <div>
    <div class="mb-2 ml-1 primary--text text-capitalize">
      {{ label }}
    </div>
    <v-autocomplete
      v-model="autocomplete"
      class="mt-0 pt-0 weight-700"
      :items="items"
      :label="hint"
    />
  </div>
</template>

<script>
export default {
  name: 'AutocompleteSelect',
  props: {
    label: {
      type: String,
      default: ''
    },
    items: {
      type: Array,
      required: true
    },
    hint: {
      type: String,
      default: 'Selecione uma opção'
    }
  },
  data () {
    return {
      autocomplete: ''
    }
  },
  watch: {
    autocomplete (value) {
      this.$emit('input', value)
    }
  }
}
</script>
