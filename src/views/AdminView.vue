<template>
  <v-container>
    <h1 class="text-center titulo-cabecera">Administración</h1>
    <div class="text-center mt-5">
      <v-btn @click="mostrarDialogoCrear" color="primary" elevation="2">Agregar Curso</v-btn>
    </div>
    <v-row>
      <v-col>
        <v-simple-table class="mt-5">
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-center">Curso</th>
                <th class="text-center">Cupos</th>
                <th class="text-center">Inscritos</th>
                <th class="text-center">Duración</th>
                <th class="text-center">Costo</th>
                <th class="text-center">Terminado</th>
                <th class="text-center">Fecha</th>
                <th class="text-center">Acciones</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="curso in cursos" :key="curso.id">
                <td class="text-center">{{ curso.nombre }}</td>
                <td class="text-center">{{ curso.cupos }}</td>
                <td class="text-center">{{ curso.inscritos }}</td>
                <td class="text-center">{{ curso.duracion }}</td>
                <td class="text-center">
                  <v-btn class="boton-inhabilitado" rounded color="success" small>${{ curso.costo }}</v-btn>
                </td>
                <td class="text-center">
                  <v-btn
                    class="boton-inhabilitado"
                    rounded
                    :color="
                      cursoTerminado(curso.id) == 'Si' ? 'info' : 'secondary'
                    "
                    small
                    >{{ cursoTerminado(curso.id) }}</v-btn>
                </td>
                <td class="text-center">
                  <v-btn class="boton-inhabilitado" rounded color="success" small>{{ curso.fecha_registro }}</v-btn>
                </td>
                <td class="text-center">
                  <v-btn icon>
                    <v-icon color="yellow darken-2" @click="$router.push(`/edit/${curso.id}`)">mdi-pencil</v-icon>
                  </v-btn>
                  <v-btn icon>
                    <v-icon @click="mostrarDialogoEliminar(curso.id)" color="red darken-3">mdi-delete</v-icon>
                  </v-btn>
                </td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
        <div class="mt-5">
          <v-alert dense outlined color="purple">
            <v-icon color="purple">mdi-account-multiple</v-icon>
            Cantidad total de alumnos permitidos:
            <strong>{{ totalAlumnosPermitidos }}</strong> alumnos.
          </v-alert>
        </div>
        <div class="mt-5">
          <v-alert dense outlined color="blue lighten-1">
            <v-icon color="blue lighten-1">mdi-account-check</v-icon>
            Cantidad total de alumnos inscritos:
            <strong>{{ totalAlumnosInscritos }}</strong> alumnos.
          </v-alert>
        </div>
        <div class="mt-5">
          <v-alert dense outlined color="red">
            <v-icon color="red">mdi-account-plus</v-icon>
            Cantidad total de cupos restantes:
            <strong>{{ TotalCuposRestantes }}</strong> alumnos.
          </v-alert>
        </div>
        <div class="mt-5">
          <v-alert dense outlined color="pink darken-2">
            <v-icon color="pink darken-2">mdi-block-helper</v-icon>
            Cantidad total de cursos terminados:
            <strong>{{ totalCursosTerminados }}</strong> cursos.
          </v-alert>
        </div>
        <div class="mt-5">
          <v-alert dense outlined color="lime darken-3">
            <v-icon color="lime darken-3">mdi-bell-ring</v-icon>
            Cantidad total de cursos activos:
            <strong>{{ totalCursosActivos }}</strong> cursos.
          </v-alert>
        </div>
        <div class="mt-5">
          <v-alert dense outlined color="amber darken-3">
            <v-icon color="amber darken-3">mdi-bell-ring</v-icon>
            Cantidad total de cursos: <strong>{{ totalCursos }}</strong> cursos.
          </v-alert>
        </div>
      </v-col>
    </v-row>
    <CrearDialogo
      @closeDialogCreate="dialogCreate = false"
      :dialogCreateProp="dialogCreate"
    />
    <EliminarDialogo
      @closeDialogDelete="dialogDelete = false"
      :dialogDeleteProp="dialogDelete"
      :idDeleteProp="idDelete"
    />
  </v-container>
</template>

<script>
import { mapState, mapGetters } from "vuex";
import CrearDialogo from "@/components/CrearDialogo.vue";
import EliminarDialogo from "@/components/EliminarDialogo.vue";

export default {
  name: "admin-view",
  data: function () {
    return {
      dialogCreate: false,
      dialogDelete: false,
      idDelete: -1,
    };
  },
  computed: {
    ...mapState(["cursos"]),
    ...mapGetters([
      "cursoTerminado",
      "totalAlumnosPermitidos",
      "totalAlumnosInscritos",
      "TotalCuposRestantes",
      "totalCursosTerminados",
      "totalCursosActivos",
      "totalCursos",
    ]),
  },
  methods: {
    mostrarDialogoCrear() {
      this.dialogCreate = true;
    },
    mostrarDialogoEliminar(id) {
      this.idDelete = id;
      this.dialogDelete = true;
    },
  },
  components: {
    CrearDialogo,
    EliminarDialogo,
  },
};
</script>

<style scoped>
/* Estilos para la vista */
</style>
