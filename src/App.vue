<template>
  <div class="container">
    <!-- modal show buttons group -->
    <div class="buttons-container">
      <button
        class="btn btnPrimary"
        v-bind="resetModals"
        @click="modalTemplateShow = !modalTemplateShow"
      >Show modal temlate</button>
      <button
        class="btn btnPrimary"
        v-bind="resetModals"
        @click="modalExemplesShow = !modalExemplesShow"
      >Show modal exemple</button>
      <button
        class="btn btnPrimary"
        v-bind="resetModals"
        @click="modalAuthorization = !modalAuthorization"
      >Show modal authorization</button>
    </div>

    <!-- modal template -->
    <ModalTemplate
      title="Modal template title"
      v-show="modalTemplateShow"
      @close="modalTemplateShow = false"
    >
      <div slot="body">
        <p>Some text</p>
        <button class="btn btnPrimary" @click="modalTemplateShow = !modalTemplateShow">Done!</button>
      </div>
    </ModalTemplate>

    <!-- modal exemles -->
    <ModalExemples
      :modalFirst="modalFirst"
      :modalSecond="modalSecond"
      :modalValidate="modalValidate"
      :sign="sign"
      v-show="modalExemplesShow"
      @clear="clearModal"
    ></ModalExemples>

    <!-- modal authorization -->
    <ModalAuthorization
      :signUpShow="signUpShow"
      :signInShow="signInShow"
      :typeOfPassword="typeOfPassword"
      :sign="sign"
      v-show="modalAuthorization"
      @clear="clearModal"
    ></ModalAuthorization>
  </div>
</template>


<script>
import ModalTemplate from "@/components/Modal/UI/ModalTemplate.vue";
import ModalExemples from "@/components/Modal-exemples/ModalExemples.vue";
import ModalAuthorization from "@/components/Modal-authorization/ModalAuthorization.vue";

export default {
  components: {
    ModalAuthorization,
    ModalExemples,
    ModalTemplate,
  },
  data() {
    return {
      modalTemplateShow: false,
      modalExemplesShow: false,
      modalAuthorization: false,
      modalFirst: false,
      modalSecond: {
        show: false,
        name: "",
        email: "",
      },
      modalValidate: false,
      signUpShow: false,
      signInShow: false,
      typeOfPassword: {
        passwordType: "password",
        repeatPasswordType: "password",
        showPassClass: "show",
        showRepPassClass: "show",
      },
      sign: {
        name: "",
        login: "",
        email: "",
        password: "",
        repeatPassword: "",
      },
    };
  },
  methods: {
    submitSecondForm() {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email,
      });
      this.modalSecond.name = "";
      this.modalSecond.email = "";
      this.modalSecond.show = false;
    },
    clearModal() {
      this.modalSecond.name = "";
      this.modalSecond.email = "";
      this.sign.name = "";
      this.sign.login = "";
      this.sign.email = "";
      this.sign.password = "";
      this.sign.repeatPassword = "";
    },
  },
  computed: {
    resetModals() {
      if (this.modalTemplateShow == true) {
        this.modalExemplesShow = false;
        this.modalAuthorization = false;
      }
      if (this.modalExemplesShow == true) {
        this.modalTemplateShow = false;
        this.modalAuthorization = false;
      }
      if (this.modalAuthorization == true) {
        this.modalTemplateShow = false;
        this.modalExemplesShow = false;
      }
    },
  },
};
</script>
<style lang="scss">
.buttons-container {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.container {
  width: 100%;
  padding: 30px 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>