<template>
  <div>
    <div class="mb-0 ml-1 primary--text">
      {{ label }}
    </div>
    <v-select
      v-model="typeSelected"
      class="mt-0"
      :items="items"
      label="Escolha uma opção"
    />
  </div>
</template>

<script>
export default {
  name: 'SelectType',
  props: {
    items: {
      type: Array,
      required: true
    },
    label: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      typeSelected: null
    }
  },
  watch: {
    typeSelected (newValue) {
      this.$emit('selected', newValue)
    }
  }
}
</script>
