<template>
    <div class="container">
        <ModalTemplate
        title="Log in"
        @close="$emit('close')">

        <div slot="body">
            <form @submit.prevent="onSignIn">
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
            <!-- require email -->
            <div class="form-item" :class="{ errorInput: $v.email.$error }">
                <label>Email:</label>
                <p class="errorText" v-if="!$v.email.required">
                        Field is required!</p>
                <p class="errorText" v-if="!$v.email.email">
                        Email is not correct!</p>
                    <input
                        v-model="email"
                        :class="{error: $v.email.$error}"
                        @change="$v.email.$touch()">
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
                          <input
                            @click="$emit('show-pass')"
                            class="show-password"
                            :class="typeOfPassword.showPassClass">
                    </div>
                </div>
                <!-- repeat password -->
                <div class="form-item" :class="{ errorInput: $v.repeatPassword.$error }">
                    <label>Repeat password</label>
                    <p class="errorText" v-if="!$v.repeatPassword.sameAsPassword.$error">Passwords must be identical.</p>
                    <div class="password-wrapper">
                      <input
                          :type="typeOfPassword.repeatPasswordType"
                          v-model="repeatPassword"
                          :class="{error: $v.repeatPassword.$error}"
                          @change="$v.repeatPassword.$touch()"/>
                          <input
                            type="button"
                            @click="$emit('show-rep-pass')"
                            class="show-password"
                            :class="typeOfPassword.showRepPassClass">
                    </div>
                </div>
            </div>
            <!-- log in button -->
            <button class="btn btnPrimary">sign in</button>
            <!-- is have account -->
            <a href="#" class="modal-auth__link" @click="$emit('change-sign-modal')">I have account</a>
            </form>
        </div>
        </ModalTemplate>
    </div>
</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'

import ModalTemplate from '../Modal/UI/ModalTemplate.vue';
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
          email: '',
          password: '',
          repeatPassword: '',
      }
  },
  validations: {
    login: {
      required,
      minLength: minLength(4)
    },
    email: {
      required,
      email
    },
    password: {
      required,
      minLength: minLength(6)
    },
    repeatPassword: {
      sameAsPassword: sameAs('password')
    }
  },
  methods: {
      onSignIn () {
          this.$v.$touch()
          if (!this.$v.$invalid) {
              const login = {
                  login: this.login,
                  email: this.email,
                  password: this.password,
              }
              const repeatPassword = this.repeatPassword
              console.log(login)

              // done
              this.login = ''
              this.email = ''
              this.password = ''
              this.repeatPassword = '',
              this.passwordType = 'password',
              this.repeatPasswordType = 'password',
              this.$v.$reset()
              this.$emit('close')
          }
      },
  }
}
</script>
