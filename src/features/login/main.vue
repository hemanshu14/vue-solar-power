<template lang="pug">
  v-container.my-login(fluid fill-height)
      v-flex.text-xs-center(xs12 lg6)
        v-layout(row wrap)
          v-flex(xs12)
            .my-login__logo-name
              img(src='~/@/assets/images/solar-panel-logo.svg' alt='VueExample')
          v-flex(xs12)
            .my-login__subheading.subheading
              | Solar Power!
          v-flex(xs12)
            v-card.my-login__card
              v-card-title.my-login__card-title(primary-title)
                v-avatar(:size="100")
                  img(src='//ssl.gstatic.com/accounts/ui/avatar_2x.png' alt='Avatar')

              v-card-text
                v-form
                  v-text-field(
                    label='E-mail'
                    v-model='credentials.username'
                    :rules="emailRules"
                    required
                  )
                  v-text-field(
                    label='Password'
                    hint='At least 8 characters'
                    v-model='credentials.password'
                    min='8'
                    :append-icon="passwordHidden ? 'visibility' : 'visibility_off'"
                    :append-icon-cb='() => (passwordHidden = !passwordHidden)'
                    :type="passwordHidden ? 'password' : 'text'"
                    counter=''
                    required
                  )

              v-card-actions.my-login__card-actions
                v-btn(
                  :loading="loading"
                  :disabled="!(credentials.username && credentials.password)"
                  @click="login()"
                  block
                  color='accent'
                  dark
                ) Login
</template>

<script>
import auth from '@/auth/helpers'

export default {
  name: 'LoginPage',

  data () {
    return {
      passwordHidden: true,
      credentials: {
        username: 'admin@admin.com',
        password: 'admin'
      },
      error: '',
      loading: false,
      emailRules: [ v => (v.match(/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/)) || 'Invalid Email address' ]
    }
  },

  methods: {
    login () {
      this.loading = true

      const credentials = {
        username: this.credentials.username,
        password: this.credentials.password
      }

      // auth.login(credentials, 'dashboard', ({isSuccess, data, errorMessage}) => {
      auth.fakeLogin(credentials, 'dashboard')
        .then((data) => {
          this.loading = false
        })
    }
  }
}
</script>

<style lang="stylus" scoped>
  .my-login
    background-color: $app-primary
    justify-content: center
    &__logo
      max-width: 46px
      padding-left: 12px
      padding-top: 4px

    &__logo-name

      img
        max-width: 200px
        width: 100%

    &__subheading
      color: black
      padding-top: 10px
      padding-bottom: 20px

    &__card
      max-width: 370px
      margin: 0 auto

    &__card-title
      justify-content: center

    &__card-actions
      justify-content: center

</style>
