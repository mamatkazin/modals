<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <!-- first modal -->
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">
            Show first modal
          </button>
          <modals
            title="First modal"
            v-show="modalFirst"
            @close="modalFirst = false"
          >
            <!-- body -->
            <div slot="body">
              <p>Text Text Text Text Text Text Text</p>
              <button class="btn btnPrimary" @click="modalFirst = !modalFirst">
                Well Done!
              </button>
            </div>
          </modals>

          <!-- second modal -->
          <button
            class="btn btnPrimary"
            @click="modalSecond.show = !modalSecond.show"
          >
            Show modal with form
          </button>
          <modals
            title="Modal with form"
            v-show="modalSecond.show"
            @close="modalSecond.show = false"
          >
            <!-- body -->
            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text" required v-model="modalSecond.name" />
                <label>Email:</label>
                <input type="email" required v-model="modalSecond.email" />
                <button class="btn btnPrimary">Submit!</button>
              </form>
            </div>
          </modals>

          <!-- modal with validate -->
          <button
            class="btn btnPrimary"
            @click="closeValidateForm(!modalValidate)"
          >
            Show modal with form + validate
          </button>
          <modalValidate
            v-show="modalValidate"
            @close="closeValidateForm(false)"
          />

          <!-- modal login -->
          <button class="btn btnPrimary" @click="closeLoginForm(!modalLogin)">
            Login
          </button>
          <modalLogin
            v-show="modalLogin"
            @close="closeLoginForm(false)"
            @registration="closeRegistrationForm(true)"
          />

          <!-- modal registration -->
          <modalRegistration
            v-show="modalRegistration"
            @close="closeRegistrationForm(false)"
          />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import modals from "@/components/UI/Modal.vue";
import modalValidate from "@/components/ModalValidate.vue";
import modalLogin from "@/components/ModalLogin.vue";
import modalRegistration from "@/components/ModalRegistration.vue";

export default {
  components: { modals, modalValidate, modalLogin, modalRegistration },
  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: "",
        email: "",
      },
      modalValidate: false,
      modalLogin: false,
      modalRegistration: false,
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

    closeValidateForm(modalValidate) {
      this.modalValidate = modalValidate;
      // this.$el.querySelector("form").reset();
    },

    closeLoginForm(modalLogin) {
      this.modalLogin = modalLogin;
    },

    closeRegistrationForm(modalRegistration) {
      this.modalRegistration = modalRegistration;
    },
  },
};
</script>
