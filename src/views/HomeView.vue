<template>
  <v-container class="site-container">
    <h1 class="text-center titulo-cabecera">Lista de Cursos</h1>
    <v-row justify="space-around" class="card-row">
      <v-card v-for="curso in cursos" :key="curso.id" class="mt-8 mx-1 cards-estilo" width="290">
        <v-img contain height="200px" :src="curso.img">
          <v-app-bar flat color="rgba(0, 0, 0, 0)"> </v-app-bar>
        </v-img>
        <h4 class="text-center mt-5">{{ curso.nombre }}</h4>
        <v-card-text>
          <div class="font-weight-bold ml-8 mb-2">Información</div>

          <v-timeline align-top dense>
            <v-timeline-item small color="deep-purple lighten-1">
              <div>
                <div class="font-weight-normal">
                <strong>Costo:</strong> ${{ curso.costo }}
                </div>
                <div><strong>Duración:</strong> {{ curso.duracion }}</div>
              </div>
            </v-timeline-item>
            <v-timeline-item small color="green">
              <div>
                <div class="font-weight-normal">
                <strong>Cupos:</strong> {{ curso.cupos }}
                </div>
                <div><strong>Completado:</strong> {{ cursoTerminado(curso.id) }}</div>
              </div>
            </v-timeline-item>
            <v-timeline-item small color="deep-purple lighten-1">
              <div>
                <div class="font-weight-normal">
                <strong>Fecha de Registro:</strong>
                </div>
                <div>{{ curso.fecha_registro }}</div>
              </div>
            </v-timeline-item>
             <v-timeline-item small color="green">
              <div>
                <div class="font-weight-normal">
                <strong>Descripción:</strong>
                </div>
                <div>{{ curso.descripcion}}</div>
              </div>
            </v-timeline-item>
          </v-timeline>
        </v-card-text>
      </v-card>
    </v-row>
  </v-container>
</template>


<script>
import { mapState, mapGetters } from "vuex";
export default {
  name: "home-view",
  data: function () {
    return {};
  },
  computed: {
    ...mapState(["cursos"]),
    ...mapGetters(["cursoTerminado"]),
  },
};
</script>

<style scoped>
</style>