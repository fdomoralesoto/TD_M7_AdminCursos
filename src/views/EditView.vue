<template>
  <v-container>
    <h1 class="text-center titulo-cabecera">Editar Curso</h1>
    <v-row>
      <v-col>
        <v-switch
          v-model="allowEdit"
          label="Editar Curso"
          color="info"
          value="info"
          hide-details=""
        ></v-switch>
        <v-form class="ma-5" ref="form" v-model="valid">
          <v-text-field
            v-model="form.nombre"
            :rules="nombreRules"
            label="Nombre"
            required
            :disabled="!allowEdit"
          ></v-text-field>

          <v-text-field
            v-model="form.img"
            :rules="imgRules"
            label="URL de la imagen"
            required
            :disabled="!allowEdit"
          ></v-text-field>

          <v-text-field
            v-model="form.cupos"
            :rules="cuposRules"
            label="Cupos del curso"
            required
            :disabled="!allowEdit"
          ></v-text-field>

          <v-text-field
            v-model="form.inscritos"
            :rules="inscritosRules"
            label="Inscritos en el curso"
            required
            :disabled="!allowEdit"
          ></v-text-field>

          <v-text-field
            v-model="form.duracion"
            :rules="duracionRules"
            label="Duración del curso"
            required
            :disabled="!allowEdit"
          ></v-text-field>

          <v-text-field
            v-model="form.fecha_registro"
            :rules="fechaRules"
            label="Fecha de registro"
            required
            :disabled="!allowEdit"
          ></v-text-field>
          <v-select
            v-model="form.completado"
            :items="types"
            :rules="completadoRules"
            label="Estado"
            required
            :disabled="!allowEdit"
          ></v-select>
  
          <v-text-field
            v-model="form.costo"
            :rules="costoRules"
            label="Costo del curso"
            required
            :disabled="!allowEdit"
          ></v-text-field>

          <v-textarea
            v-model="form.descripcion"
            :rules="descripcionRules"
            :disabled="!allowEdit"
          >
            <template v-slot:label>
              <div>Descripción del curso</div>
            </template>
          </v-textarea>

          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4 mb-4"
            @click="editarCurso"
          >
            Editar
          </v-btn>

          <v-btn
            color="error"
            class="mr-4 mb-4"
            @click="$router.push('/admin')"
          >
            Cerrar
          </v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  name: "edit-view",
  props: {
    id: {
      type: String,
      required: true,
    },
  },
  data: function () {
    return {
      form: {
        nombre: "",
        img: "",
        cupos: "",
        inscritos: "",
        duracion: "",
        fecha_registro: new Date().toLocaleDateString("es-CL"),
        costo: "",
        descripcion: "",
        completado: false,
      },
      valid: true,
      allowEdit: false,
      types: [{text:"Activo", value:false}, {text:"Terminado", value:true}],
      nombreRules: [(v) => !!v || "El nombre del curso es requerido"],
      imgRules: [(v) => !!v || "La URL de la imagen es requerida"],
      cuposRules: [
        (v) => !!v || "Los cupos disponibles del curso son requeridos",
      ],
      inscritosRules: [
        (v) => !!v || "La cantidad de inscritos en el curso es requerida",
        (v) => {
          if (Number(v) >= Number(this.form.cupos)) {
            return "La cantidad de inscritos debe ser menor o igual a los cupos disponibles";
          } else {
            return true;
          }
        },
      ],
      duracionRules: [(v) => !!v || "La duración del curso es requerida"],
      fechaRules: [(v) => !!v || "La fecha del curso es requerida"],
      completadoRules: [
        (v) => {
          if (v == true) {
            this.form.inscritos = "0";
          }
          return true;
        },
      ],
      costoRules: [(v) => !!v || "El costo del curso es requerido"],
      descripcionRules: [(v) => !!v || "La descripción del curso es requerida"],
    };
  },
  computed: {
    ...mapGetters(["obtenerCurso"]),
  },
  methods: {
    ...mapActions(['editar_curso']),
    validate() {
      this.$refs.form.validate();
    },
    editarCurso() {
      this.$refs.form.validate();
      this.editar_curso(this.form);
      this.$router.push('/admin')
    },
    
  },
  created() {
    this.form = this.obtenerCurso(this.id);
  },
};
</script>

<style scoped>
</style>