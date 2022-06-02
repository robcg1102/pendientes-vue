<template>
  <div class="row">
    <ProgresBar :porcentaje="porcentaje" :proyectos="proyectos" />
    <div class="col-4">
      <form @submit.prevent="crearProyecto">
        <div class="mb-3">
          <label for="proyecto" class="form-label">Proyecto</label>
          <input
            type="text"
            class="form-control"
            id="proyecto"
            v-model.trim="proyecto"
            required
          />
        </div>
        <div class="mb-3">
          <label for="actividad" class="form-label">Actividad</label>
          <select
            id="actividad"
            class="form-select"
            v-model="actividad"
            required
          >
            <option disabled selected value="">Seleccione un tipo</option>
            <option>App Web con Vue</option>
            <option>Backend con Node</option>
            <option>App Movil con Native</option>
          </select>
        </div>
        <div class="mb-3">
          <label for="urgente" class="form-check-label">Urgente</label>
          <input
            type="checkbox"
            class="form-check-input"
            id="urgente"
            v-model="urgente"
          />
        </div>
        <button type="submit" class="btn btn-primary">Guardar</button>
      </form>
    </div>
    <TableProject
      :numeroProyectos="numeroProyectos"
      :proyectos="proyectos"
      :delProyecto="delProyecto"
      :cambiarUrgente="cambiarUrgente"
    />
  </div>
</template>

<script>
import ProgresBar from "./ProgresBar.vue";
import TableProject from "./TableProject.vue";
export default {
  data: () => ({
    proyecto: "",
    actividad: "",
    urgente: false,
    proyectos: [],
  }),
  computed: {
    numeroProyectos() {
      return this.proyectos.length;
    },
    porcentaje() {
      let completados = 0;
      this.proyectos.map((proye) => {
        if (proye.urgente === false) completados++;
      });
      return (completados * 100) / this.numeroProyectos || 0;
    },
  },
  methods: {
    crearProyecto() {
      const formProyecto = {
        proyecto: this.proyecto,
        actividad: this.actividad,
        urgente: this.urgente,
      };
      this.proyectos.push(formProyecto);
      this.saveData();
      this.proyecto = "";
      this.urgente = false;
      this.actividad = "";
    },
    delProyecto(indice) {
      this.proyectos.splice(indice, 1);
      this.saveData();
    },
    cambiarUrgente(i) {
      this.proyectos[i].urgente = !this.proyectos[i].urgente;
      this.saveData();
    },
    saveData() {
      localStorage.setItem("proyectos", JSON.stringify(this.proyectos));
    },
  },
  components: { ProgresBar, TableProject },
  mounted() {
    this.proyectos = JSON.parse(localStorage.getItem("proyectos")) || [];
  },
};
</script>

<style>
.changeButton:hover {
  cursor: pointer;
}
</style>