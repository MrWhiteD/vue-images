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
        <span>{{group}} {{ items[0].NAME }}</span>
      </td>
    </template>
    <template v-slot:item="{ item }">
      <tr v-for="item1 in item.SKU">
        <td>{{ item1.ID }}</td>
        <td>{{ item1.NAME }}</td>
        <template v-if="item1.PICTURE.single">
          <td>
            <image-cell :img_url="item1.PICTURE"/>
          </td>
        </template>
        <template v-else>
          <td width="500px">
            <v-select
                :items="Object.entries(item1.PICTURE)"
                item-text="NAME"
                item-value="NAME"
                label="Select"
                persistent-hint
                return-object
                single-line
                @change="itemSel"
                v-model="yb_model"
            >
              <template v-slot:item="{ item }">
                <span v-for="item in item">{{ item.NAME }}</span>
              </template>
              <template v-slot:selection="{item}">
                {{item[1].NAME}}
              </template>
            </v-select>
            <image-cell v-model="yb_model[1]"/>
          </td>
        </template>
      </tr>
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
      { text: "Dessert (100g serving)", value: "name" },
      { text: "Calories", value: "calories" },
      { text: "Fat (g)", value: "fat" },
    ],
    desserts: [{
      "28670" : {"PROD_ID": "28670", "NAME" : "сумка женская Olivi ол694"},
      "33468" : {"PROD_ID": "33468", "NAME" : "сумка женская Olivi ол729"},
      "53363" : {"PROD_ID": "53363", "NAME" : "сумка женская Olivi ол837"},
  }],
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
      ebus.$emit('hi', this.yb_model[1].PICTURE)
      //this.emit('fun', this.yb_model)
    },
  },
}
</script>
<style scoped>

</style>