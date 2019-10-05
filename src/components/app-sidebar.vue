<template lang="pug">
  v-navigation-drawer.my-sidebar(
    v-model="isActive"
    fixed
    :mobile-break-point="1904"
    app
    touchless
    dark
  )
    v-layout(justify-center wrap)
      // img.my-sidebar__backdrop(src='~/@/assets/images/Sun.jpg' alt='Vue Solar Power')
      .my-sidebar__hero-pattern

    v-divider

    v-avatar.my-sidebar__avatar(:size="70")
      img(src='//ssl.gstatic.com/accounts/ui/avatar_2x.png' alt='Avatar')

    v-list(dark)
      v-list-group(prepend-icon='person')
        v-list-tile(slot="activator" ripple)
          v-list-tile-content
            v-list-tile-title {{ $store.state.auth.user.name }}
        v-list-tile(ripple :to="{ name: 'account' }")
          v-list-tile-action
            v-icon account_box
          v-list-tile-content
            v-list-tile-title Account
        v-list-tile(ripple :to="{ name: 'settings' }")
          v-list-tile-action
            v-icon settings
          v-list-tile-content
            v-list-tile-title Settings

    v-divider
    v-list(dark)
      v-list-tile(ripple :to="{ name: 'tutorial' }")
        v-list-tile-action
          v-icon library_books
        v-list-tile-content
          v-list-tile-title Tutorial

      v-list-tile(ripple :to="{ name: 'dashboard' }")
        v-list-tile-action
          v-icon dashboard
        v-list-tile-content
          v-list-tile-title Dashboard

      v-list-group(prepend-icon='build')
        v-list-tile(slot="activator" ripple)
          v-list-tile-content
            v-list-tile-title Tools
        v-list-tile(ripple :to="{ name: 'budgetTool' }")
          v-list-tile-content
            v-list-tile-title Budget Analyzer
        v-list-tile(ripple :to="{ name: 'rateTool' }")
          v-list-tile-content
            v-list-tile-title Rate Adjuster

      v-list-group(prepend-icon='assessment')
        v-list-tile(slot="activator" ripple)
          v-list-tile-content
            v-list-tile-title Reports
        v-list-tile(ripple :to="{ name: 'laborReport' }")
          v-list-tile-content
            v-list-tile-title Labor Report
        v-list-tile(ripple :to="{ name: 'earningsReport' }")
          v-list-tile-content
            v-list-tile-title Earnings

      v-list-group(prepend-icon='web')
        v-list-tile(slot="activator" ripple)
          v-list-tile-content
            v-list-tile-title Examples
        v-list-tile(ripple :to="{ name: 'wip' }")
          v-list-tile-content
            v-list-tile-title Work-in-progress

      v-list-group(prepend-icon='more_horiz')
        v-list-tile(slot="activator" ripple)
          v-list-tile-content
            v-list-tile-title More
        v-list-tile(ripple :to="{ name: 'importMyData' }")
          v-list-tile-content
            v-list-tile-title More Here

      v-list-tile(@click="logout()" ripple)
        v-list-tile-action
          v-icon exit_to_app
        v-list-tile-content
          v-list-tile-title Log out
</template>

<script>
import auth from '@/auth/helpers'

export default {
  name: 'AppSidebar',

  computed: {
    isActive: {
      get () {
        return this.$store.state.common.sidebar.visible
      },
      set (val) {
        this.$store.dispatch('common/updateSidebar', { visible: val })
      }
    }
  },

  methods: {
    logout () {
      auth.logout()
    }
  }
}
</script>

<style lang="stylus">
  .my-sidebar
    z-index: 8

    &__logo
      padding-right: 10px
      padding-top: 14px
      padding-bottom: 14px
      height: 60px

    &__hero-pattern
      height: 145px
      width: 300px
      position: absolute
      background-color: #1a88ff

    &__avatar
      margin-top: 15px
      margin-left: 15px
</style>
