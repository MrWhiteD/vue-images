<template>
  <v-app>

    <v-main>
      <main-table/>
    </v-main>
  </v-app>
</template>

<script>

import MainTable from "@/components/main-table";
export default {
  name: 'App',

  components: {
    MainTable
  },

  data: () => ({
    desserts1: [{
      "28670" : {"PROD_ID": "28670", "NAME" : "сумка женская Olivi ол694"},
      "33468" : {"PROD_ID": "33468", "NAME" : "сумка женская Olivi ол729"},
      "53363" : {"PROD_ID": "53363", "NAME" : "сумка женская Olivi ол837"},
    }],
    desserts2: [
      {"PROD_ID": "28670", "NAME" : "сумка женская Olivi ол694"},
      {"PROD_ID": "33468", "NAME" : "сумка женская Olivi ол729"},
      {"PROD_ID": "53363", "NAME" : "сумка женская Olivi ол837"},
    ],

    fff:[]
  }),
};

</script>
