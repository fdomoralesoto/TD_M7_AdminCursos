<template>
  <div class="text-center">
    <v-dialog :value="dialogDeleteProp" width="500">
      <v-card>
        <v-card-title class="text-h6 white--text deep-purple accent-4">
          Eliminar Curso
        </v-card-title>

        <v-card-text class="mt-3">
          ¿Está seguro que desea eliminar el curso?
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="success" class="mr-4" @click="eliminarCurso()"> Aceptar </v-btn>
          <v-btn color="primary" @click="closeDialogDelete">Cerrar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import {mapState, mapActions} from 'vuex'
export default {
  name: "dialogDelete-component",
  props: {
    dialogDeleteProp: {
      type: Boolean,
      required: true,
    },
    idDeleteProp:{
      type: Number,
      required: true,
    }
  },
  data: function () {
    return {};
  },
  computed: {
    ...mapState(['cursos']),
  },
  methods: {
    closeDialogDelete() {
      this.$emit("closeDialogDelete");
    },
    eliminarCurso() {
      this.eliminar_curso(this.idDeleteProp)
      this.closeDialogDelete();
    },
    ...mapActions(['eliminar_curso']),
  },
};
</script>

<style scoped>
</style>