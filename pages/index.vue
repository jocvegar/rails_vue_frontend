<template>
  <b-container class="bv-example-row mt-5">
    <b-list-group 
      v-for="example in examples" 
      :key="example.id" 
      class="text-center text-white">
          <b-list-group-item class="my-1" :style="{backgroundColor: example.colour}">{{example.name}}</b-list-group-item>
    </b-list-group>
  </b-container>
</template>

<script>
export default {
  data () {
    return {
      examples: []
    }
  },
  methods: {
    async updateExamples() {
      this.examples = await this.$axios.$get('/examples')
    }
  },
  mounted () {
    this.updateExamples()
  }
}
</script>
