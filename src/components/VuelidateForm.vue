<template>
  <div class="root">
    <h2 class="title-form">Crie sua conta aqui</h2>
    <p>
      <input type="text" placeholder="Email" v-model="state.email" />
      <span v-if="v$.email.$error"> {{ v$.email.$errors[0].$message }}</span>
    </p>
    <p>
      <input
        type="password"
        placeholder="Senha"
        v-model="state.password.password"
      />
      <span v-if="v$.password.password.$error">
        {{ v$.password.password.$errors[0].$message }}</span
      >
    </p>
    <p>
      <input
        type="password"
        placeholder="Confirme sua Senha"
        v-model="state.password.confirm"
      />
      <span v-if="v$.password.confirm.$error">
        {{ v$.password.confirm.$errors[0].$message }}</span
      >
    </p>
    <button class="btn" @click="submitForm">Enviar</button>
  </div>
</template>

<script>
import useValidate from "@vuelidate/core";
import { reactive } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";
import { required, email, minLength, sameAs, helpers } from "@vuelidate/validators";

export default {
  setup() {
    const state = reactive({
      email: "",
      password: {
        password: "",
        confirm: ""
      },
    });

    const mustBeLearnVue = (value) => value.includes('learnvue')

    const rules = computed(() => {
      return {
        email: { required, email, mustBeLearnVue:helpers.withMessage('E-mail é válido', mustBeLearnVue) },
        password: {
          password: { required, minLength: minLength(6) },
          confirm: { required, sameAs: sameAs(state.password.password) },
        },
      };
    });

    const v$ = useValidate(rules, state);

    return {
      state,
      v$,
    };
  },

  methods: {
    submitForm() {
      this.v$.$validate(); // checks all inputs
      if (!this.v$.$error) {
        // if ANY fail validation
        alert("Formulário enviado com sucesso!");
      } else {
        alert("Formulário inválido");
      }
    },
  },
};
</script>

<style lang="css">
.root {
  width: 400px;
  margin: 0 auto;
  background-color: #fff;
  padding: 30px;
  margin-top: 160px;
  border-radius: 10px;
  text-align: center;
}

.title-form {
  font-weight: 600;
}

input {
  border: none;
  outline: none;
  border-bottom: 1px solid #ddd;
  font-size: 1em;
  padding: 5px 0;
  margin: 10px 0 5px 0;
  width: 100%;
}

.btn {
  background-color: #3498db;
  padding: 10px 20px;
  margin-top: 10px;
  border: none;
  color: white;
  font-weight: 700;
  text-transform: uppercase;
  border-radius: 5px;
  font-size: 1em;
  cursor: pointer;
}

.btn:hover {
  transition-duration: 0.5s;
  background-color:#236d9e;
}
</style>
