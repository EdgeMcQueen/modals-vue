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
                          :type="passwordType"
                          v-model="password"
                          :class="{error: $v.password.$error}"
                          @change="$v.password.$touch()">
                          <button @click="showPassword" class="show-password" :class="showPassClass"></button>
                    </div>
                </div>
                <!-- repeat password -->
                <div class="form-item" :class="{ errorInput: $v.repeatPassword.$error }">
                    <label>Repeat password</label>
                    <p class="errorText" v-if="!$v.repeatPassword.sameAsPassword.$error">Passwords must be identical.</p>
                    <div class="password-wrapper">
                      <input
                          :type="repeatPasswordType"
                          v-model="repeatPassword"
                          :class="{error: $v.repeatPassword.$error}"
                          @change="$v.repeatPassword.$touch()"/>
                          <button @click="showPasswordRepeat" class="show-password" :class="showRepPassClass"></button>
                    </div>
                </div>
            </div>
            <!-- log in button -->
            <button class="btn btnPrimary">log in</button>
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
    data() {
      return {
          login: '',
          email: '',
          password: '',
          repeatPassword: '',
          passwordType: 'password',
          repeatPasswordType: 'password',
          showPassClass: 'show',
          showRepPassClass: 'show'
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
      showPassword() {
        if (this.passwordType == 'password') {
          this.passwordType = 'text'
          this.showPassClass = 'hide'
          }
        else {
          this.passwordType = 'password'
          this.showPassClass = 'show'
        }
      },
      showPasswordRepeat() {
        if (this.repeatPasswordType == 'password') {
          this.repeatPasswordType = 'text'
          this.showRepPassClass = 'hide'
          }
        else {
          this.repeatPasswordType = 'password'
          this.showRepPassClass = 'show'
        }
      },
  }
}
</script>
<style lang="scss">
  .password-wrapper {
    position: relative;
  }
  .show-password {
    z-index: 990;
    position: absolute;
    top: 8px;
    right: 20px;
    width: 40px;
    height: 40px;
    border: none;
    background: none;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    &.show {
      background-image: url('../../assets/icons/eye.png');
    }
    &.hide {
      background-image: url('../../assets/icons/eye-hidden.png');
    }
  }
</style>