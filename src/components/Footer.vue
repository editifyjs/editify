<template>
  <v-footer dark padless>
    <v-card
      width="100%"
      color="#435b71"
      flat
      tile
      class="white--text text-center"
    >
      <v-card-text>
        <v-btn
          v-for="(item, i) in buttons"
          :key="i"
          class="mx-4 white--text"
          :href="item.url"
          target="_blank"
          icon
        >
          <v-icon size="24px">
            {{ item.icon }}
          </v-icon>
        </v-btn>
      </v-card-text>

      <v-card-text class="white--text pt-0">
        Modern, block-style, completely free (MIT license) and pioneering Vue
        editor &#128081;
        <br />
        <br />
        Developed by Omer Celik &#128155;&#128153;
      </v-card-text>

      <v-divider></v-divider>

      <v-card-text class="white--text">
        © {{ new Date().getFullYear() }} — <strong>Editify.js</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>

<script>
export default {
  data: () => ({
    buttons: [
      { icon: "mdi-github", url: "https://github.com/oclk" },
      { icon: "mdi-linkedin", url: "https://www.linkedin.com/in/oclk" },
      { icon: "mdi-instagram", url: "https://www.instagram.com/repomine" },
    ],
  }),
};
</script>