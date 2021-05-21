<template>
  <v-app style="background: linear-gradient(90deg, rgba(41,226,230,1) 0%, rgba(18,221,79,1) 61%, rgba(75,160,211,1) 100%); background: linear-gradient(0deg, rgba(0,252,255,1) 0%, rgba(179,181,215,1) 55%, rgba(32,180,215,1) 100%); background: linear-gradient(0deg, rgba(0,252,255,1) 0%, rgba(85,126,225,1) 55%, rgba(32,85,215,1) 100%); " >
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      title: 'Vuetify.js'
    }
  }
}
</script>
