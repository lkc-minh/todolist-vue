<template>
  <v-app>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
import "vue-toast-notification/dist/theme-sugar.css";
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
