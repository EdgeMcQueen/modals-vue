<template>
  <div class="container">
    <ModalTemplate title="Log in" @close="$emit('close')" v-bind="formData">
      <div slot="body">
        <form @submit.prevent="onSignUp">
          <!-- require login -->
          <div class="form-item" :class="{ errorInput: $v.login.$error }">
            <label>Login:</label>
            <p class="errorText" v-if="!$v.login.required">Field is required!</p>
            <p
              class="errorText"
              v-if="!$v.login.minLength"
            >Login must have at least {{ $v.login.$params.minLength.min }} !</p>
            <input
              v-model="sign.login"
              :class="{error: $v.login.$error}"
              @change="$v.login.$touch()"
            />
          </div>
          <!-- password -->
          <div>
            <div class="form-item" :class="{ errorInput: $v.password.$error }">
              <label>Password:</label>
              <p class="errorText" v-if="!$v.password.required">Password is required.</p>
              <p
                class="errorText"
                v-if="!$v.password.minLength"
              >Password must have at least {{ $v.password.$params.minLength.min }} letters.</p>
              <div class="password-wrapper">
                <input
                  :type="typeOfPassword.passwordType"
                  v-model="sign.password"
                  :class="{error: $v.password.$error}"
                  @change="$v.password.$touch()"
                />
                <input
                  type="button"
                  @click="$emit('show-pass')"
                  class="show-password"
                  :class="typeOfPassword.showPassClass"
                />
              </div>
            </div>
          </div>
          <!-- log in button -->
          <button class="btn btnPrimary">sign up</button>
          <!-- is haven't account -->
          <a href="#" class="modal-auth__link" @click="$emit('change-sign-modal')">I need to account</a>
        </form>
      </div>
    </ModalTemplate>
  </div>
</template>

<script>
import ModalTemplate from "../Modal/UI/ModalTemplate.vue";
import { required, minLength, email } from "vuelidate/lib/validators";

export default {
  components: {
    ModalTemplate,
  },
  props: {
    typeOfPassword: {
      type: Object,
      required: true,
    },
    sign: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      login: "",
      password: "",
    };
  },
  validations: {
    login: {
      required,
      minLength: minLength(4),
    },
    password: {
      required,
      minLength: minLength(6),
    },
  },
  methods: {
    onSignUp() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        const login = {
          login: this.sign.login,
          password: this.sign.password,
        };
        console.log(login);

        // done
        this.sign.login = "";
        this.sign.password = "";
        (this.passwordType = "password"), this.$v.$reset();
        this.$emit("close");
      }
    },
  },
  computed: {
    formData() {
      this.login = this.sign.login;
      this.email = this.sign.email;
      this.password = this.sign.password;
      this.repeatPassword = this.sign.repeatPassword;
    },
  },
};
</script>