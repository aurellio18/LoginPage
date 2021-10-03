<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
      dense
    >
    <router-link to="/" tag="span">
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="../src/assets/api.png"
          transition="scale-transition"
          width="25"
        />

        <v-toolbar-title style="font-size:20px;">Ini Aplikasi</v-toolbar-title>
      </div>
      </router-link>

      <v-spacer></v-spacer>

      <router-link to="/register" tag="span">
      <v-btn text>
        <span>Register</span>
      </v-btn>
      </router-link>
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
