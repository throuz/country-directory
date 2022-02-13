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

        <v-simple-table>
          <tbody>
            <tr v-for="(value, name, i) in countryData" :key="i">
              <template
                v-if="typeof value === 'object' && !Array.isArray(value)"
              >
                <td>{{ name }}</td>
                <td class="pr-0 pl-0">
                  <v-simple-table>
                    <tbody>
                      <tr v-for="(value2, name2, j) in value" :key="j">
                        <template
                          v-if="
                            typeof value2 === 'object' && !Array.isArray(value2)
                          "
                        >
                          <td>{{ name2 }}</td>
                          <td class="pr-0 pl-0">
                            <v-simple-table>
                              <tbody>
                                <tr
                                  v-for="(value3, name3, k) in value2"
                                  :key="k"
                                >
                                  <template
                                    v-if="
                                      typeof value3 === 'object' &&
                                      !Array.isArray(value3)
                                    "
                                  >
                                    <td>{{ name3 }}</td>
                                    <td class="pr-0 pl-0">
                                      <v-simple-table>
                                        <tbody>
                                          <tr
                                            v-for="(value4, name4, l) in value3"
                                            :key="l"
                                          >
                                            <td>{{ name4 }}</td>
                                            <td>{{ value4 }}</td>
                                          </tr>
                                        </tbody>
                                      </v-simple-table>
                                    </td>
                                  </template>
                                  <template v-else>
                                    <td>{{ name3 }}</td>
                                    <td>{{ value3 }}</td>
                                  </template>
                                </tr>
                              </tbody>
                            </v-simple-table>
                          </td>
                        </template>
                        <template v-else>
                          <td>{{ name2 }}</td>
                          <td>{{ value2 }}</td>
                        </template>
                      </tr>
                    </tbody>
                  </v-simple-table>
                </td>
              </template>
              <template v-else>
                <td>{{ name }}</td>
                <td>{{ value }}</td>
              </template>
            </tr>
          </tbody>
        </v-simple-table>

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
export default {
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

<style scoped>
td {
  border-left: thin solid rgba(0, 0, 0, 0.12);
}
</style>