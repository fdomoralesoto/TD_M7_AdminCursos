<template>
  <div>
    <v-app-bar
      color="purple accent-4"
      dense
      dark
    >
      <!-- <v-toolbar-title class="titulo-home">Cursos AlfaWeb</v-toolbar-title> -->
      <v-toolbar-title class="titulo-home">
      <router-link to="/">Cursos AlfaWeb</router-link>
      </v-toolbar-title>

      <v-spacer></v-spacer>
      <div class="botones-header">
      <v-btn to="/" class="nav-icon-button" icon>
        <v-icon class="nav-icon">mdi-home</v-icon>
      </v-btn>
      <v-btn to="/admin" class="nav-icon-button" icon>
        <v-icon class="nav-icon" color="white">mdi-wrench</v-icon>
      </v-btn>
      </div>

    </v-app-bar>
  </div>
</template>

<script>
export default {
    name: 'navbar-component',
    data: function(){
        return {}
    },
}
</script>

<style scoped>
</style>