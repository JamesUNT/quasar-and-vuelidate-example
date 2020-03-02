<template>
  <q-page>
    <modal></modal>
  </q-page>
</template>

<script>
import LoginForm from '../components/LoginVuelidate'
export default {
  name: 'PageIndex',
  components: {
    modal: LoginForm
  }
}
</script>
