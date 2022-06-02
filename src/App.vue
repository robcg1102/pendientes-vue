<template>
  <div class="m-4">
    <h1>Pendientes</h1>
    <hr />
    <formVue />
  </div>
</template>

<script>
import FormVue from "./components/FormVue.vue";
export default {
  data: () => ({
    formulario: {
      nombre: "",
      edad: 15,
      mail: "",
    },
  }),
  methods: {
    addUser() {
      console.log(this.formulario);
    },
  },
  components: {
    FormVue,
  },
};
</script>

<style>
</style>