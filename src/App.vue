<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="App Logo"
          class="shrink mr-2"
          contain
          src="src/assets/logo.svg"
          transition="scale-transition"
          width="40"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="/"
        text
      >
        <span class="mr-2">Выход</span>
        <v-icon>mdi-exit-to-app</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <AdminPage />
    </v-main>
  </v-app>
</template>

<script>
import AdminPage from './pages/AdminPage';

export default {
  name: 'App',

  components: {
    AdminPage,
  },

  data: () => ({
    //
  }),
};
</script>
