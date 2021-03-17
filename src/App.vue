<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">

          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
          <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show modal with form</button>
          <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show modal with form + validate</button>


          <modals
            title="First modal"
            v-show="modalFirst"
            @close="modalFirst = false">

            <div slot="body">
              <p>Text Tesxt</p>
             <button class="btn btnPrimary" @click="modalFirst = false">Well done</button>
            </div>

          </modals>

           <modals
            title="Second modal"
            v-show="modalSecond.show"
            @close="modalSecond.show = false, modalSecond.name = '', modalSecond.email = ''"

            >

            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text" v-model="modalSecond.name" required >
                <label>Email:</label>
                <input type="email" v-model="modalSecond.email" required>
                <button class="btn btnPrimary">Submit</button>
              </form>
             
            </div>

          </modals>

          <modalValidate v-show="modalValidate" @close="modalValidate = false, name = ''" />
        </div>
      </section>
    </div>
  </div>
</template>

<script>

import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'

export default {
  components: {
    modals,
    modalValidate
  },
  data () {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: '',
      },
      modalValidate: false
    }
  },
  methods: {
    submitSecondForm() {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      })
      this.modalSecond.name = '',
      this.modalSecond.email = '',
      this.modalSecond.show = false
    }
  }
}
</script>

<style>

</style>
