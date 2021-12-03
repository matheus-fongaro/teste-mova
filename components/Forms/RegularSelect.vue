<template>
  <div>
    <div class="mb-2 ml-1 primary--text text-capitalize">
      {{ label }}
    </div>
    <v-select
      v-model="selectedType"
      class="mt-0 pt-0"
      :items="items"
      :label="hint"
    />
  </div>
</template>

<script>
export default {
  name: 'SelectType',
  props: {
    value: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    hint: {
      type: String,
      default: 'Escolha uma opção'
    },
    items: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      selectedType: ''
    }
  },
  watch: {
    selectedType (newValue) {
      this.$emit('input', newValue)
    }
  }
}
</script>
