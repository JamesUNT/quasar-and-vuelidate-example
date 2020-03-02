<template>
  <q-page class="row justify-center q-py-md">
    <div class="col-4">
      <q-card class="row justify-center">
        <q-card-section class="col-10">
          <q-input class="column" color="indigo-10" dense filled v-model.trim="email" label="Ex: thiago.silva@quasar.org"
          :rules="[ val => $v.email.required || 'Email obrigatório.', // Aplicando as regras importadas do vuelidate
          val => $v.email.email || 'Formato de email inválido.' ]"
          >
            <template v-slot:before>
              <span class="text-body2">E-mail:</span>
            </template>
          </q-input>
          <q-input type="number" class="column" color="indigo-10" dense filled v-model.trim="senha" @input="setarSenhaLocal($event.target.value)"
          :rules="[ val => $v.senha.numeric && $v.senha.integer || 'Somente números inteiros.' ]"
          >
            <template v-slot:before>
              <span class="text-body2">Senha:</span>
            </template>
          </q-input>
        </q-card-section>
        <q-card-section class="col-5">
          <q-btn class="full-width" color="indigo-10" label="Primary" />
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import { mapActions, mapState } from 'vuex'
import { required, email, numeric, integer } from 'vuelidate/lib/validators'

export default {
  name: 'loginVuelidate',
  data () {
    return {
      email: '',
      senha: ''
    }
  },
  methods: {
    ...mapActions('example', ['setarSenha']),
    setarSenhaLocal (value) {
      // Caso precisa validar algo cujo os dados estão numa state.js, você precisará criar um método que venha a executar a action necessária;
      // por que você precisará usar o $touch() para funcionar.
      this.setarSenha(value)
      this.$v.senha.$touch()
    }
  },
  computed: {
    ...mapState('example', ['senha'])
  },
  validations: {
    email: {
      required,
      email
    },
    senha: {
      required,
      numeric,
      integer
    }
  }
}
</script>
