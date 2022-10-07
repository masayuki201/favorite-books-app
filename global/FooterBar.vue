<template>
<div>
  <v-footer
      color="primary lighten-1"
      padless
  >
    <v-row
        justify="center"
        no-gutters
    >
      <v-btn
          v-for="link in links"
          :key="link"
          color="white"
          text
          rounded
          class="my-2"
      >
        {{ link }}
      </v-btn>
      <v-col
          class="primary lighten-1 py-4 text-center white--text"
          padless
          cols="12"
      >
        {{ new Date().getFullYear() }} — <strong>Favorite-Books-App</strong>
      </v-col>
    </v-row>
  </v-footer>
</div>
</template>

<script>
export default {
  name: "FooterBar",
  data(){
    return{
      links: [
        'Home',
        'About Us',
        'Team',
        'Services',
        'Blog',
        'Contact Us',
      ],
    }
  }
}
</script>

<style scoped>

</style>
