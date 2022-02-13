<template>
  <v-simple-table>
    <tbody>
      <tr v-for="(value, name, i) in tableData" :key="i">
        <template v-if="typeof value === 'object' && !Array.isArray(value)">
          <td>{{ name }}</td>
          <td class="pr-0 pl-0 no-border-left">
            <DetailsTable :tableData="value" />
          </td>
        </template>
        <template v-else>
          <td>{{ name }}</td>
          <td>{{ Array.isArray(value) ? value.join(" 、") : value }}</td>
        </template>
      </tr>
    </tbody>
  </v-simple-table>
</template>

<script>
export default {
  name: "DetailsTable",

  props: {
    tableData: {
      type: Object,
      default: () => ({}),
    },
  },
};
</script>

<style scoped>
td {
  border-left: thin solid rgba(0, 0, 0, 0.12);
}
.no-border-left {
  border-left: none;
}
</style>