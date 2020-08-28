<template>
    <div class="container">
         <!-- first modal -->
        <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
        <ModalTemplate
        title="Firt modal"
        v-show="modalFirst"
        @close="modalFirst = false">

        <div slot="body">
            <p>some text</p>
            <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well done!</button>
        </div>
        </ModalTemplate>

        <!-- second modal -->
        <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show form modal</button>
        <ModalTemplate
        title="Modal with form"
        v-show="modalSecond.show"
        @close="modalSecond.show = false">

        <div slot="body">
            <form @submit.prevent="submitSecondForm">
            <label>Name:</label>
                <input type="text" v-model="modalSecond.name" required>
            <label>Email:</label>
                <input type="email" v-model="modalSecond.email" required>
            <button class="btn btnPrimary">Submit</button>
            </form>
        </div>
        </ModalTemplate>

        <!-- modal with validate -->
        <button class="btn btnPrimary" @click="validModal = !validModal">Show modal with form + validate</button>
        <ModalValidate v-show="validModal" @close="validModal = false"/>
    </div>
</template>

<script>
import ModalTemplate from '../Modal/UI/ModalTemplate.vue';
import ModalValidate from './ModalValidate.vue';

export default {
  components: {
    ModalValidate,
    ModalTemplate,
  },
  props: {
      modalFirst: {
          type: Boolean,
          required: true
      },
      modalSecond: {
          type: Object,
          required: true
      },
      modalValidate: {
          type: Boolean,
          required: true
      }
  },
  data() {
      return {
          validModal: this.modalValidate
      }
  },
}
</script>