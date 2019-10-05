<template lang="pug">
v-container.my-dashboard(
  fluid
  fill-height
  text-xs-center
  v-bind:grid-list-sm="$vuetify.breakpoint.smAndDown"
  v-bind:grid-list-lg="$vuetify.breakpoint.mdAndUp"
)
  v-layout(row wrap)

    // Top Row
    v-flex(d-flex xs12 sm12 md6)
      v-card
        v-card-title
          .title Energy Production
        v-card-text(style="position: relative; height: 100%; max-height: 400px;")
          chart(style="height: 100%;")
    v-flex(d-flex xs12 sm12 md6)
      v-card.my-dashboard__energy-status
        v-card-title
          .title Average Hourly Energy Production
        v-card-text
          v-layout(row wrap)
            v-flex(xs4)
              .sub-title CO2 Emission Savings
            v-flex(xs4)
              .sub-title Equivalent Trees Saved
            v-flex(xs4)
              .sub-title Yield Today
            v-flex(d-flex xs4)
              v-progress-circular.my-dashboard__order(
                :size="100"
                :width="15"
                :rotate="360"
                :value="45"
                color="#1a8cff"
              )
                | 632.02 T

            v-flex(d-flex xs4)
              v-progress-circular(
                :size="100"
                :width="15"
                :rotate="360"
                :value="75"
                color="accent"
              )
                | 2.14 Tree

            v-flex(d-flex xs4)
              v-progress-circular(
                :size="100"
                :width="15"
                :rotate="360"
                :value="15"
                color="#4da6ff"
              )
                | 6.2 kWh
            v-flex(d-flex xs12)
              line-chart(style="height: 200px; width: 100%;")

    // Bottom Row
    v-flex(d-flex xs12 sm12 md6)
      v-card
        v-card-title
          .title(style="margin-bottom: 15px;") Todo
        v-date-picker(
          v-model="date"
          min="2016-06-15"
          max="2020-03-20"
          full-width
          class="picker__title__color"
          :event-color="date => date[9] % 2 ? 'red' : 'yellow'"
          :events="functionEvents"
        )
    v-flex(d-flex xs12 sm12 md6)
      v-card
        v-card-media(src="static/images/mountains.png" height="200px")
          v-layout.my-dashboard__media(column)
            v-card-title(class="white--text pl-5 pt-5")
              .display-1.pl-5.pt-5 Main Contacts
        v-list(two-line)
          v-list-tile(@click="")
            v-list-tile-action
              v-icon phone
            v-list-tile-content
              v-list-tile-title (+31) 6131-70349
              v-list-tile-sub-title Mobile

</template>

<script>
import store from './store' // eslint-disable-line no-unused-vars
import Chart from './components/chart'
import LineChart from './components/line-chart'

export default {
  name: 'Dashboard',

  components: {
    Chart,
    LineChart
  },

  data () {
    return {
      test: this.$store.state.dashboard.test,
      date: '2019-05-21'
    }
  },

  mounted () {
  },

  methods: {
    updateTest () {
      this.test++
      this.$store.dispatch('dashboard/updateTest', this.test)
    },
    functionEvents (date) {
      const [,, day] = date.split('-')
      return parseInt(day, 10) % 3 === 0
    }
  }
}
</script>

<style lang="stylus">
.my-dashboard

  &__media
    height: 100%
    margin: 0

  .picker__title
    display: none !important
  .primary
    background-color: #1a88ff !important
    border-color: #1a88ff !important
</style>
