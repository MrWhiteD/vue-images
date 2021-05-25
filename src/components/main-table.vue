<template>
  <v-container>
    <v-data-table
        :headers="headers"
        :items="desserts"
        group-by="PROD_ID"
    >
      <template v-slot:group.header="{group, items, isOpen, toggle}">
        <td :colspan="headers.length">
          <v-icon @click="toggle">
            {{ isOpen ? 'mdi-minus' : 'mdi-plus' }}
          </v-icon>
          <span>{{ group }} {{ items }} - {{ items[0].ARTICLE }}</span>
        </td>
      </template>
      <template v-slot:item="{items}" v-for="sss in items">
      </template>
    </v-data-table>
  </v-container>
</template>

<script>
import ImageCell from "@/components/image-cell";
import {ebus} from "@/main";

export default {
  name: "main-table",
  components: {ImageCell},
  data: () => ({
    yb_model: [{0:"2", 1:[{"NAME":"", "PICTURE":[]}]}],
    headers: [
      { text: "Dessert ", value: "ID" },
      { text: "Calories", value: "SKU" },
      { text: "Fat (g)", value: "SKU.PICTURE" },
    ],
    desserts: [],
  }),
  mounted() {
    fetch('https://uralgalant.ru/bitrix/php_interface/include/utils/index.php')
    .then(response => response.json())
    .then(json => {this.desserts = Object.values(json)})
  },
  methods: {
    modItem (item) {
      return Object.values(item)
    },
    itemSel(itm) {
      console.log(this.yb_model)
      ebus.$emit('hi'+itm, this.yb_model[1].PICTURE)
      //this.emit('fun', this.yb_model)
    },
  },
}
</script>
<style scoped>

</style>