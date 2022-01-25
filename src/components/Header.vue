<template>
  <v-card
    class="mx-auto overflow-hidden card-header"
    height="auto"
    width="385"
  >

    <v-app-bar
      color="deep-purple accent-4"
      dark
      
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Menu</v-toolbar-title>

      <v-spacer></v-spacer>

      <!-- <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-filter</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn> -->
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      fixed
      bottom
      temporary
    >
      <v-list
        nav
        dense
      >
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-title>Inicio</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>Consumo de aparelhos</v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>Ajuda</v-list-item-title>
          </v-list-item>

        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>

 
  </v-card>
</template>

<script>
  export default {
    data: () => ({
      drawer: false,
      group: null,
    }),

    watch: {
      group () {
        this.drawer = false
      },
    },
  }
</script>


<style scoped>
.card-header {
    margin: 0 10px;
}
   
</style>
