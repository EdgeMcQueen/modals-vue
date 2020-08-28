<template>
    <div class="modal-auth">
        <!-- sign up -->
        <input type="button" @click="showSignUp = !showSignUp" value="Sign up">
        <ModalSignUp
            v-show="showSignUp"
            @close="showSignUp = false"
            :typeOfPassword="typeOfPassword"
            @show-pass="showPassword"
            @change-sign-modal="changeSignModal"/>

        <!-- sign in -->
        <input type="button" @click="showSignIn = !showSignIn" value="Sign in">
        <ModalSignIn
            v-show="showSignIn"
            @close="showSignIn = false"
            :typeOfPassword="typeOfPassword"
            @show-pass="showPassword"
            @show-rep-pass="showPasswordRepeat"
            @change-sign-modal="changeSignModal"/>
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
      changeSignModal () {
          this.showSignIn = !this.showSignIn
          this.showSignUp = !this.showSignUp
      }
  },
}
</script>
<style lang="scss">
    .modal-auth {
        display: flex;
        justify-content: flex-end;
        padding: 30px 0;
    }
    .change-modal {
        display: block;
        width: fit-content;
        margin: 20px auto;
        border-bottom: 1px solid black;

        &:visited {
            color: black;
        }
    }
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