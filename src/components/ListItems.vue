<template>
  <v-container v-if="list.length>0">
    <v-row dense>
      <v-col v-for="(item, idx) in list" :key="idx" cols="12" style="max-width:450px;margin:auto">
        <v-card>
          <div class="d-flex flex-no-wrap justify-space-between">
            <v-avatar class="ma-3" size="125" tile>
              <v-img v-if="item.image!==undefined" :src="item.image.src"></v-img>
            </v-avatar>
            <div>
              <v-card-title v-text="item.title"></v-card-title>
              <v-card-subtitle v-text="item.id"></v-card-subtitle>
            </div>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "ListItems",
  props: {
    list:Array
  },
  data: () => ({
    lookFor: "",
    searchEnabled: false,
    //list: [{}],
  }),
  watch: {
    lookFor(val) {
      this.searchEnabled = val && true;
    },
  },
  methods: {
    doSearch() {
      if (this.lookFor ?? false) {
        console.log("doSearch for : ", this.lookFor);
      }
    },
  },
  mounted(){
    console.log("List:",this.list);
  }
};
</script>
<style scoped>
.mt {
  font-size: 18px;
}
</style>