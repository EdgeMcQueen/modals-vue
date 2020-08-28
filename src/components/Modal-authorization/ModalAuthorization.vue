<template>
    <div class="container">
        <button class="btn btnPrimary" @click="showSignIn = !showSignIn">Sign in</button>
        <ModalSignIn
            v-show="showSignIn"
            @close="showSignIn = false"/>
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
          showSignIn: this.signInShow
      }
  },
}
</script>