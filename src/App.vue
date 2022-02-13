<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row class="text-center">
          <v-col cols="12">
            <SearchResults />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import SearchResults from "./components/SearchResults";

export default {
  name: "App",

  components: {
    SearchResults,
  },

  data: () => ({
    //
  }),
};
</script>
