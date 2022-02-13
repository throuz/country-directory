<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="60%">
      <template v-slot:activator="{ on, attrs }">
        <v-btn v-bind="attrs" v-on="on" small depressed>
          {{ countryName }}
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Country Details
        </v-card-title>

        <DetailsTable :tableData="countryData" />

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="dialog = false"> Close </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import DetailsTable from "./DetailsTable";

export default {
  name: "Details",

  components: {
    DetailsTable,
  },

  props: {
    countryName: {
      type: String,
      default: "",
    },
    countryData: {
      type: Object,
      default: () => ({}),
    },
  },

  data() {
    return {
      dialog: false,
    };
  },
};
</script>
