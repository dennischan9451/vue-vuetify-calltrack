<template>
  <v-app-bar
    app
    color="secondary"
    dark
    class="px-3"
  >
    <div class="d-flex align-center">
      <a href="/">
        <v-img
          alt="Dashboard Logo"
          class="shrink mr-2"
          contain
          src="@/assets/img/dashboard-logo.png"
          transition="scale-transition"
          width="100"
        />
      </a>
    </div>

    <v-spacer></v-spacer>

    <div class="d-inline-flex align-center">
      <span class="body-1 mr-1">Hello, Dev</span>
      <v-btn
        text
        class="px-0"
      >
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </div>
  </v-app-bar>
</template>
