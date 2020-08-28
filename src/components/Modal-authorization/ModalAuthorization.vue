<template>
    <div class="container">
        <button class="btn btnPrimary" @click="showSignIn = !showSignIn">Sign in</button>
        <ModalSignIn
            v-show="showSignIn"
            @close="showSignIn = false"
            :typeOfPassword="typeOfPassword"
            @show-pass="showPassword"
            @show-rep-pass="showPasswordRepeat"/>
    </div>
</template>

<script>
import ModalTemplate from '../Modal/UI/ModalTemplate.vue';
import ModalSignIn from './ModalSignIn.vue';
export default {
  components: {
    ModalSignIn,
    ModalTemplate,
  },
  props: {
      signInShow: {
          type: Boolean,
          required: true
      }
  },
  data() {
      return {
          showSignIn: this.signInShow,
          typeOfPassword: {
            passwordType: 'password',
            repeatPasswordType: 'password',
            showPassClass: 'show',
            showRepPassClass: 'show'
          }
      }
  },
  methods: {
      showPassword() {
        if (this.typeOfPassword.passwordType == 'password') {
          this.typeOfPassword.passwordType = 'text'
          this.typeOfPassword.showPassClass = 'hide'
          }
        else {
          this.typeOfPassword.passwordType = 'password'
          this.typeOfPassword.showPassClass = 'show'
        }
      },
      showPasswordRepeat() {
        if (this.typeOfPassword.repeatPasswordType == 'password') {
          this.typeOfPassword.repeatPasswordType = 'text'
          this.typeOfPassword.showRepPassClass = 'hide'
          }
        else {
          this.typeOfPassword.repeatPasswordType = 'password'
          this.typeOfPassword.showRepPassClass = 'show'
        }
      },
  },
}
</script>