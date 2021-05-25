<template>
  <v-sheet
      class="mx-auto"
      max-width="400"
  >
    <v-slide-group
        v-model="model"
        class="pa-4"
        show-arrows
    >
      <v-slide-item
          v-for="n in local_img_url"
          :key="n"
          v-slot="{ active, toggle }"
      >
        <v-card
            :color="active ? 'primary' : 'grey lighten-1'"
            class="ma-4"
            height="100"
            width="100"
            @click="toggle"
        >
          <v-img :src="n"/>
        </v-card>
      </v-slide-item>
    </v-slide-group>
  </v-sheet>
</template>

<script>
import {ebus} from "@/main";

export default {
  props:['img_url', 'cell_id'],
  name: "image-cell",
  data: () => ({
    model: null,
    local_img_url: null,
  }),
  created() {
    this.local_img_url = this.img_url
    console.log(this.cell_id)
    ebus.$on('hi'+this.cell_id, (data) =>{this.local_img_url = data})
  },
  methods:{
    fun() {
      console.log("this.yb_model[1].PICTURE")
    },
  },
}
</script>

<style scoped>

</style>