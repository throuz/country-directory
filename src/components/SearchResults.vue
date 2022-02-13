<template>
  <v-card>
    <v-card-title>
      國家目錄
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="desserts"
      :search="search"
      :footer-props="{
        'items-per-page-options': [25, 50, 100],
      }"
      :items-per-page="25"
      :loading="isLoading"
    >
      <template v-slot:[`item.flags.png`]="{ item }">
        <v-img
          :src="item.flags.png"
          :alt="item.name.official"
          height="20px"
          width="25px"
        ></v-img>
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      isLoading: true,
      search: "",
      headers: [
        {
          text: "國旗",
          align: "start",
          sortable: false,
          value: "flags.png",
        },
        { text: "國家名稱", value: "name.official" },
        { text: "2位國家代碼", value: "cca2" },
        { text: "3位國家代碼", value: "cca3" },
        { text: "母語名稱", value: "name.nativeNames", width: "25%" },
        { text: "替代國家名稱", value: "altNames", width: "25%" },
        { text: "國際電話區號", value: "idds" },
      ],
      desserts: [],
    };
  },

  created() {
    fetch("https://restcountries.com/v3.1/all")
      .then((response) => response.json())
      .then((data) => {
        data.forEach((item) => {
          item.name.nativeNames = "";
          if (item.name.nativeName) {
            for (const key in item.name.nativeName) {
              const nativeName = item.name.nativeName[key]["official"];
              if (item.name.nativeNames === "") {
                item.name.nativeNames = nativeName;
              } else {
                item.name.nativeNames += `、${nativeName}`;
              }
            }
          }

          item.altNames = "";
          if (item.altSpellings.length) {
            item.altSpellings.forEach((name) => {
              if (item.altNames === "") {
                item.altNames = name;
              } else {
                item.altNames += `、${name}`;
              }
            });
          }

          item.idds = "";
          if (Object.keys(item.idd).length) {
            item.idd.suffixes.forEach((suffix) => {
              const idd = item.idd.root + suffix;
              if (item.idds === "") {
                item.idds = idd;
              } else {
                item.idds += `、${idd}`;
              }
            });
          }
          // Because there are too many idds in the United States
          if (item.idds.length > 23) {
            item.idds = item.idds.slice(0, 23);
            item.idds += "...";
          }
        });

        this.desserts = data;
        this.isLoading = false;
      });
  },
};
</script>