<template>
  <v-app>
    <v-app-bar style="height: 62px" app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Tooliıo Logo"
          class="shrink mr-2"
          contain
          src="/logo.png"
          transition="scale-transition"
          width="40"
        />
      </div>
      <span class="align-center">Toolio Shop</span>
      <v-spacer></v-spacer>
    </v-app-bar>
    <v-main>
      <v-row class="text-center">
        <v-col cols="12">
          <v-img src="logo-large.png" class="my-3" contain height="100" />
        </v-col>
      </v-row>
      <search-bar @onSearch="search"></search-bar>
      <list-items v-if="list !== undefined" :list="list"></list-items>
    </v-main>
    <v-overlay :value="overlay">
      <v-progress-circular indeterminate size="64"></v-progress-circular>
    </v-overlay>
  </v-app>
</template>

<script>
import ListItems from "./components/ListItems.vue";
import SearchBar from "./components/SearchBar.vue";

export default {
  name: "App",

  components: {
    ListItems,
    SearchBar
  },
  methods: {
    search(val) {
      console.log("Search-Event:", val);
      this.searchAndFilter(val);
    },
    async searchAndFilter(val) {
      this.overlay=true;
      let response = await fetch( "http://localhost:3005/searchProductByTitle?title=" + val); 
      //let response = await fetch("sample_response.json");
      let resJson = await response.json();
      console.log(resJson);
      this.list = resJson;
      this.overlay=false;
      //this.list = this.list.products.filter((x) => x.title.includes(val));
    },
  },
  data: () => ({
    list: [],
    overlay:false
    //
  }),
};
</script>
