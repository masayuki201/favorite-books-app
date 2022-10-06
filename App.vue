<template>
  <v-app>
    <HeaderBar/>
    <v-main>
      <router-view/>
    </v-main>
    <FooterBar/>
  </v-app>
</template>

<script>

import HeaderBar from "@/global/HeaderBar";
import FooterBar from "@/global/FooterBar";
export default {
  name: 'App',
  components: {
    FooterBar,
    HeaderBar,
  },
  data: () => ({
    //
  }),
};
</script>
