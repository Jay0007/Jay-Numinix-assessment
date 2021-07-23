<template>
  <v-container class="pa-5">
    <v-row class="mt-15" >
      <v-col cols="12" sm="6" md="4">
        <v-text-field
          label="Find customers"
          hide-details
          flat
          solo
          prepend-inner-icon="mdi-magnify"
          v-model="searchByName"
        ></v-text-field>
      </v-col>

      <v-spacer></v-spacer>
      
      <v-col cols="6" sm="4" md= "3" class=" ml-auto ">
        <v-select
          :itemx="items"
          label="Filter by Name (A-Z)"
          flat
          solo
          v-model="sortByName"
        ></v-select>
      </v-col>
    </v-row>
    <v-row class="mt-5">
      <v-col v-for="obj in filteredList" :key="obj.id" md="3" cols="12">
        <CustomerCard :customerProp="obj"></CustomerCard>
      </v-col>
      <h3 v-if="!filteredList.length">
        No customer(s) found with the search criteria.
      </h3>
    </v-row>
  </v-container>
</template>

<script>
import CustomerCard from "./card/index.vue";
export default {
  components: {
    CustomerCard,
  },
  data: () => ({
    cards: [],
    searchByName: "",
    sortByName: "",
    items: ["Name (A-Z)", "Name (Z-A)"],
  }),
  created() {
    this.$axios
      .get("http://jsonplaceholder.typicode.com/users")
      .then((response) => {
        this.cards = response.data;
        this.cards.map(function (entry) {
          try {
            var imgPath = require("../assets/images/" + entry.name + ".jpg"); // eslint-disable-line no-undef
          } catch (err) {
            imgPath = require("../assets/images/default.jpg"); // eslint-disable-line no-undef
          }
          entry.image = imgPath;
          return entry;
        });
      })
      .catch((err) => console.log(err.message));
  },
  methods: {
    filterCustomersByName: function (cards) {
      let alphaArr = cards.filter((card) => {
        return card.name
          .toLowerCase()
          .includes(this.searchByName.toLowerCase());
      });
      return alphaArr;
    },

    sortCustomersByName: function (cards) {
      if (this.sortByName == "Name (A-Z)") {
        let alphaArr = cards.sort((cust1, cust2) => {
          if (cust1["name"] == cust2["name"]) {
            return 0;
          }
          return cust2["name"] > cust1["name"] ? -1 : 1;
        });
        return alphaArr;
      } else if (this.sortByName == "Name (Z-A)") {
        let alphaArr = cards.sort((cust1, cust2) => {
          if (cust1["name"] == cust2["name"]) {
            return 0;
          }
          return cust2["name"] < cust1["name"] ? -1 : 1;
        });
        return alphaArr;
      } else {
        return cards;
      }
    },
  },
  computed: {
    filteredList: function () {
      return this.sortCustomersByName(this.filterCustomersByName(this.cards));
    },
  },
};
</script>
