<template>
  <div class="container">
    <div class="buttons-container">
    <button class="btn btnPrimary" @click="modalTemplateShow = !modalTemplateShow">Show modal temlate</button>
    <button class="btn btnPrimary" @click="modalExemplesShow = !modalExemplesShow">Show modal exemple</button>
    <button class="btn btnPrimary" @click="modalAuthorization = !modalAuthorization">Show modal exemple</button>
    </div>
    <!-- modal template -->
    <ModalTemplate
      title="Modal template title"
      v-show="modalTemplateShow"
      @close="modalTemplateShow = false">

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
      v-show="modalExemplesShow">

    </ModalExemples>
    <!-- modal authorization -->
    <ModalAuthorization
      :signInShow="signInShow"
      v-show="modalAuthorization">

    </ModalAuthorization>
  </div>
</template>


<script>
import ModalTemplate from '@/components/Modal/UI/ModalTemplate.vue';
import ModalExemples from '@/components/Modal-exemples/ModalExemples.vue';
import ModalAuthorization from '@/components/Modal-authorization/ModalAuthorization.vue';

export default {
  components: {
    ModalAuthorization,
    ModalExemples,
    ModalTemplate
  },
  data() {
    return {
      modalTemplateShow: false,
      modalExemplesShow: false,
      modalAuthorization: false,
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: ''
      },
      modalValidate: false,
      signInShow: false
    }
  },
  methods: {
    submitSecondForm () {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      })
      this.modalSecond.name = ''
      this.modalSecond.email = ''
      this.modalSecond.show = false

    }
  },

}
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