<template>
  <modal title="Войти 👋" @close="close">
    <!-- body -->
    <div slot="body">
      <div class="mb-6">
        <form name="form-validate" @submit.prevent="onSubmit">
          <div class="mb-4 form-item" :class="{ errorInput: $v.name.$error }">
            <label
              for="l-login"
              class="block text-gray-500 text-sm font-bold mb-2"
              >Логин:</label
            >
            <p class="errorText" v-if="!$v.name.required">Filed is required!</p>
            <p class="errorText" v-if="!$v.name.minLength">
              Name must have at least {{ $v.name.$params.minLength.min }} !
            </p>
            <input
              v-model="name"
              :class="{ error: $v.name.$error }"
              @change="$v.name.$touch()"
              id="l-login"
              class="shadow appearance-none b-800 rounded w-full h-12 py-2 px-3 leading-tight"
            />
          </div>
          <div
            class="mb-4 form-item"
            :class="{ errorInput: $v.password.$error }"
          >
            <label
              for="l-password"
              class="block text-gray-500 text-sm font-bold mb-2"
              >Пароль:</label
            >
            <p class="errorText" v-if="!$v.password.required">
              Filed is required!
            </p>
            <p class="errorText" v-if="!$v.password.minLength">
              Name must have at least {{ $v.password.$params.minLength.min }} !
            </p>
            <input
              type="password"
              v-model="password"
              :class="{ error: $v.password.$error }"
              @change="$v.password.$touch()"
              id="l-password"
              class="shadow appearance-none b-800 rounded w-full h-12 py-2 px-3 leading-tight"
            />
          </div>
          <button
            class="bg-blue-200 text-gray-980 font-bold w-full h-12 py-2 px-4 rounded"
          >
            Войти
          </button>
        </form>
      </div>
      <div class="modal-footer">
        <a class="text-blue" @click="$emit('registration')"
          >Мне нужен аккаунт</a
        >
      </div>
    </div>
  </modal>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";

import modal from "@/components/UI/ModalNew.vue";

export default {
  components: { modal },
  data() {
    return {
      name: "",
      password: "",
    };
  },
  validations: {
    name: {
      required,
      minLength: minLength(4),
    },
    password: {
      required,
      minLength: minLength(6),
    },
  },
  methods: {
    close() {
      this.name = "";
      this.password = "";

      this.$v.$reset();
      this.$emit("close");
    },

    onSubmit(e) {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        const user = {
          name: this.name,
          password: this.password,
        };

        console.log(user);
        this.close();
      }
    },
  },
};
</script>

<style lang="scss">
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13.4px;
  color: #de4040;
}
.form-item {
  &.errorInput .errorText {
    display: block;
  }
}
input.error {
  border-color: #de4040;
}

.modal-footer {
  padding: 0.6rem 0;
  text-align: center;
  font-size: 0.8rem;
  background-color: #f2f3f5;
}

.text-blue {
  cursor: pointer;
  font-size: 0.875rem;
  color: #5c9ce6;
}

.mb-6 {
  margin-bottom: 1.5rem;
}

.mb-4 {
  margin-bottom: 1rem;
}

.b-800 {
  border: 1px solid #e1e3e6;
}
.w-full {
  width: 100%;
}

.shadow {
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
}
.px-3 {
  padding-left: 0.75rem;
  padding-right: 0.75rem;
}
.py-2 {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}
.leading-tight {
  line-height: 1.25;
}
.h-12 {
  height: 3rem;
}
.rounded {
  border-radius: 0.25rem;
}

.text-sm {
  font-size: 0.875rem;
}
.text-gray-500 {
  color: #8f9398;
}
.mb-2 {
  margin-bottom: 0.5rem;
}
.font-bold {
  font-family: "HelveticaNeueCyr-Bold", "Helvetica", "Arial", sans-serif;
}

input {
  background-color: rgb(232, 240, 254) !important;
  background-image: none !important;
  color: -internal-light-dark(black, white) !important;
}

.text-gray-980 {
  color: #f9f9f9;
}
.px-4 {
  padding-left: 1rem;
  padding-right: 1rem;
}

.bg-blue-200 {
  cursor: pointer;
  background-color: #5c9ce6;
}

.bg-blue-200:hover {
  background-color: #5181b8;
}

.block {
  text-align: left;
}
</style>
