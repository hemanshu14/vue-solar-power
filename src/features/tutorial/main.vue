<template lang="pug">
v-container.my-tutorial(fluid fill-height text-xs-center)
  v-layout(justify-center align-center)
    v-flex.my-tutorial__hero(text-xs-center)
      div
        |Check out the tutorial on the project's Github.
        br
        br
      div
        v-btn(
          color="primay"
          href="https://github.com/hemanshu14/vue-solar-power"
          target="_blank"
        ) Go to Tutorial

</template>

<script>
export default {
  name: 'Wip',

  data () {
    return {
    }
  },

  mounted () {
  },

  methods: {

  }
}
</script>

<style lang="stylus" scoped>
.my-wip

  &__hero
    opacity 0.4

  &__cone
    width 100px

</style>
