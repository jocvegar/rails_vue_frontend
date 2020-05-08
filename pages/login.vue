<template>
    <b-container class="mt-5">
      <h4 class="text-center">HOLA</h4>
      <b-card v-if="$auth.$state.loggedIn">
          <b-alert :show="error != null" variant="danger" :value="error" dismissible>{{error}}</b-alert>
          <b-card-text>
              Logged in as {{$auth.$state.user.email}}
          </b-card-text>
          <br>
          <b-button @click="logout" variant="primary">Log out</b-button>
      </b-card>
      <b-card v-else>
          <b-alert :show="error != null" variant="danger" :value="error" dismissible>{{error}}</b-alert>
          <b-card-text>
              <b-form>
                  <b-form-input v-model="email" type="email" required placeholder="Enter email" />
                  <br>
                  <b-form-input v-model="password" type="password" required placeholder="Password" />
              </b-form>
                  <br>
              <b-button @click="login" variant="primary">Log In</b-button>
          </b-card-text>
      </b-card>
    </b-container>
</template>

<script>
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    login: function () {
      this.$auth.login({
        data: {
          user: {
            email: this.email,
            password: this.password
          }
        }
      }).catch(e => {this.error = e + ''})
    },
    logout: function () {
      this.$auth.logout().catch(e => {this.error = e + ''})
    }
  }
}
</script>
