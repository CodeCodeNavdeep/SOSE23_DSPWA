<template>
  <div>
    <p @click="loadAddress(user.id)">{{ user }}</p>
  </div>
  <div v-if="addresses.length > 0">
    <div v-for="address in addresses" :key="address.id">
        <AddressDetail :address="address"></AddressDetail> 
    </div> 

    
    <v-expansion-panels>
      <v-expansion-panel>
      <v-expansion-panel-title>
        {{ user.firstname +user.lastname }}
      </v-expansion-panel-title>
        <v-expansion-panels>
          <v-expansion-panel
            v-for="address in addresses" :key="address.id"
            :title="address.street" 
            :text="address.number"
          ></v-expansion-panel>
        </v-expansion-panels>
      </v-expansion-panel>
    </v-expansion-panels>
    
  
  </div>
</template>

<script>
import axios from "axios";

import AddressDetail from './AddressDetail.vue'

export default {
  components: { AddressDetail },
  props: {
    user: {},
  },
  data() {
    return {
      addresses: [],
    };
  },
  methods: {
    async loadAddress(userId) {
      var addresses = await axios.get(
        "http://localhost:3000/addresses?userId=" + userId
      );
      addresses.data.forEach((address) =>
        console.log(address.street + " " + address.number)
      );
      this.addresses = addresses.data;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  color: #b9425c;
}
</style>