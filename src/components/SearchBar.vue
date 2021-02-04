<template>
  <v-container style="position: sticky;
    top: -4px;
    z-index: 5;">
    <v-row>
      <v-col style="max-width:320px;margin:auto;">
        <v-text-field
          v-model="lookFor"
          center
          label="Seach Product"
          solo
          @keydown.enter="doSearch()"
        ></v-text-field>
        <v-icon style="position:absolute; margin-top:-66px; margin-left:250px" @click="doSearch()">mdi-card-search-outline</v-icon>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "SearchBar",

  data: () => ({
    lookFor: "",
    searchEnabled: false,
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
        this.$emit("onSearch",this.lookFor);
      }
    },
  },
};
</script>
<style>
.v-icon{
  position:absolute;
  margin-top:-66px;
  margin-left:250px
}
</style>