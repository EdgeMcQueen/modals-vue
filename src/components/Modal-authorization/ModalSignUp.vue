<template>
    <div class="container">
        <ModalTemplate
        title="Log in"
        @close="$emit('close')">

        <div slot="body">
            <form @submit.prevent="onSignUp">
            <!-- require login -->
            <div class="form-item" :class="{ errorInput: $v.login.$error }">
                <label>Login:</label>
                <p class="errorText" v-if="!$v.login.required">
                        Field is required!</p>
                <p class="errorText" v-if="!$v.login.minLength">
                        Login must have at least {{ $v.login.$params.minLength.min }} !</p>
                    <input
                        v-model="login"
                        :class="{error: $v.login.$error}"
                        @change="$v.login.$touch()">
            </div>
            <!-- password -->
            <div>
                <div class="form-item" :class="{ errorInput: $v.password.$error }">
                    <label>Password:</label>
                    <p class="errorText" v-if="!$v.password.required">Password is required.</p>
                    <p class="errorText" v-if="!$v.password.minLength">Password must have at least {{ $v.password.$params.minLength.min }} letters.</p>
                    <div class="password-wrapper">
                      <input
                          :type="typeOfPassword.passwordType"
                          v-model="password"
                          :class="{error: $v.password.$error}"
                          @change="$v.password.$touch()">
                          <button @click="$emit('show-pass')" class="show-password" :class="typeOfPassword.showPassClass"></button>
                    </div>
                </div>
            </div>
            <!-- log in button -->
            <button class="btn btnPrimary">sign up</button>
            </form>
        </div>
        </ModalTemplate>
    </div>
</template>

<script>
import ModalTemplate from '../Modal/UI/ModalTemplate.vue';
import { required, minLength, email } from 'vuelidate/lib/validators'

export default {
  components: {
    ModalTemplate,
  },
  props: {
    typeOfPassword: {
      type: Object,
      required: true
    }
  },
  data() {
      return {
          login: '',
          password: '',
      }
  },
    validations: {
    login: {
      required,
      minLength: minLength(4)
    },
    password: {
      required,
      minLength: minLength(6)
    },
  },
      methods: {
      onSignUp () {
          this.$v.$touch()
          if (!this.$v.$invalid) {
              const login = {
                  login: this.login,
                  password: this.password,
              }
              console.log(login)

              // done
              this.login = ''
              this.password = ''
              this.passwordType = 'password',
              this.$v.$reset()
              this.$emit('close')
          }
      },
  }
}
</script>