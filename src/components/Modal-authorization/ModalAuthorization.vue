<template>
    <div class="container">
        <!-- sign up -->
        <button class="btn btnPrimary" @click="showSignUp = !showSignUp">Sign up</button>
        <ModalSignUp
            v-show="showSignUp"
            @close="showSignUp = false"
            :typeOfPassword="typeOfPassword"
            @show-pass="showPassword"/>

        <!-- sign in -->
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
import ModalSignUp from './ModalSignUp.vue';
export default {
  components: {
    ModalSignUp,
    ModalSignIn,
    ModalTemplate,
  },
  props: {
      signUpShow: {
          type: Boolean,
          required: true
      },
      signInShow: {
          type: Boolean,
          required: true
      }

  },
  data() {
      return {
          showSignUp: this.signUpShow,
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
<style lang="scss">
  .password-wrapper {
    position: relative;
  }
  .show-password {
    z-index: 999;
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