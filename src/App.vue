<template>
<VuelidateForm />
</template>

<script>
import VuelidateForm from './components/VuelidateForm.vue'

export default {
  name: 'App',
  components: {
    VuelidateForm
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500;600&family=Poppins:wght@400;700&display=swap');

body {
  background-color: #42b983;
}

* {
  font-family: 'Montserrat', sans-serif;
}
</style>
