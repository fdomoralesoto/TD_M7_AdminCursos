<template>
  <div class="text-center">
    <v-dialog :value="dialogCreateProp" width="900">
      <v-card>
        <v-card-title class="text-h6 white--text deep-purple accent-4">
          Agregar Curso
        </v-card-title>
        <v-form class="ma-5" ref="form" v-model="valid">
          <v-text-field
            v-model="form.nombre"
            label="Nombre"
            required
            :rules="nombreRules"
          ></v-text-field>

          <v-text-field
            v-model="form.img"
            label="URL de la imagen"
            required
            :rules="imgRules"
          ></v-text-field>

          <v-text-field
            v-model="form.cupos"
            label="Cupos del curso"
            required
            :rules="cuposRules"
          ></v-text-field>

          <v-text-field
            v-model="form.inscritos"
            label="Inscritos en el curso"
            required
            :rules="inscritosRules"
          ></v-text-field>

          <v-text-field
            v-model="form.duracion"
            label="Duración del curso"
            required
            :rules="duracionRules"
          ></v-text-field>

          <v-text-field
            v-model="form.fecha_registro"
            label="Fecha de registro"
            required
            :rules="fechaRules"
            disabled
          ></v-text-field>

          <v-text-field
            v-model="form.costo"
            label="Costo del curso"
            required
            :rules="costoRules"
          ></v-text-field>

          <v-textarea
            v-model="form.descripcion"
            required
            :rules="descripcionRules"
          >
            <template v-slot:label>
              <div>Descripción del curso</div>
            </template>
          </v-textarea>

          <v-btn
            :disabled="!valid"
            color="success"
            class="mr-4 mb-4"
            @click="crearCurso"
          >
            Agregar
          </v-btn>

          <v-btn color="warning" class="mr-4 mb-4" @click="reset">
            Limpiar Formulario
          </v-btn>

          <v-btn color="error" class="mb-4" @click="closeDialogCreate">
            Cancelar
          </v-btn>
        </v-form>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
export default {
  name: "name-component",
  props: {
    dialogCreateProp: {
      type: Boolean,
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

      nombreRules: [(v) => !!v || "El nombre del curso es requerido"],
      imgRules: [(v) => !!v || "La URL de la imagen es requerida"],
      cuposRules: [
        (v) => !!v || "Los cupos disponibles del curso son requeridos",
      ],
      inscritosRules: [
        (v) => !!v || "La cantidad de inscritos en el curso es requerida",
        (v) => {
          if (Number(v) > Number(this.form.cupos)) {
            return "La cantidad de inscritos debe ser menor o igual a los cupos disponibles";
          } else {
            return true;
          }
        },
      ],
      duracionRules: [(v) => !!v || "La duración del curso es requerida"],
      fechaRules: [(v) => !!v || "La fecha del curso es requerida"],
      costoRules: [(v) => !!v || "El costo del curso es requerido"],
      descripcionRules: [(v) => !!v || "La descripción del curso es requerida"],
    };
  },
  computed: {
    ...mapState(["cursos"]),
  },
  methods: {
    ...mapActions(["agregar_curso"]),
    closeDialogCreate() {
      this.$emit("closeDialogCreate");
    },
    validate() {
      this.$refs.form.validate();
    },
    reset() {
      this.$refs.form.reset();
    },
    resetValidation() {
      this.$refs.form.resetValidation();
    },
    crearCurso() {
      this.$refs.form.validate();
      this.form.id = this.idRandom(50, 300)
      this.agregar_curso(this.form);
      this.closeDialogCreate();
    },
    idRandom(minVal, maxVal) {
      var randVal = minVal + Math.random() * (maxVal - minVal);
      return Math.round(randVal);
    },
  },
};
</script>

<style scoped>
</style>