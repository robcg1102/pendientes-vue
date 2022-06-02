<template>
  <div class="col-8">
    <p>Número de proyectos: {{ numeroProyectos }}</p>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Proyecto</th>
          <th scope="col">Actividad</th>
          <th scope="col">Urgente</th>
          <th scope="col">Eliminar</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(uniPro, i) in proyectos" :key="i" class="align-middle">
          <th scope="row">{{ i + 1 }}</th>
          <td>{{ uniPro.proyecto }}</td>
          <td>{{ uniPro.actividad }}</td>
          <td
            @click="cambiarUrgente(i)"
            :class="uniPro.urgente ? 'bg-danger' : 'bg-success'"
            class="text-center changeButton"
          >
            {{ uniPro.urgente ? "SI" : "NO" }}
          </td>
          <th scope="col" class="text-center">
            <button class="btn btn-danger btn-lg" @click="delProyecto(i)">X</button>
          </th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ["numeroProyectos", "proyectos", "delProyecto", "cambiarUrgente"],
};
</script>
