<template>
  <div class="container">
    <div class="buttons-container">
    <button class="btn btnPrimary" @click="modalTemplateShow = !modalTemplateShow">Show modal temlate</button>
    <button class="btn btnPrimary" @click="modalExemplesShow = !modalExemplesShow">Show modal exemple</button>
    <button class="btn btnPrimary" @click="modalExemplesShow = !modalExemplesShow">Show modal exemple</button>
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
  </div>
</template>


<script>
import ModalTemplate from '@/components/Modal/UI/ModalTemplate.vue';
import ModalExemples from '@/components/Modal-exemples/ModalExemples.vue';

export default {
  components: {
    ModalExemples,
    ModalTemplate
  },
  data() {
    return {
      modalTemplateShow: false,
      modalExemplesShow: false,
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: ''
      },
      modalValidate: false
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
</style>