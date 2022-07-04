<template>
  <div class="container">
    <div class="row">
      <div class="input-group mb-3">
        <input type="text" class="form-control" v-model="searchTerm" placeholder="Enter beer name" aria-describedby="basic-addon2">
        <div class="input-group-append">
        <button class="btn btn-outline-secondary" type="button" @click="getApiData(searchTerm)">Search for beers</button>
        </div>
      </div>
    </div>
  </div>
  <template v-if="beerList">
    <table class="table table-hover">
      <tbody>
      <tr>
        <th scope="col" class="text-start">Name</th>
        <th scope="col" class="text-start">First brewed</th>
        <th scope="col" class="text-start">Description</th>
        <th scope="col" class="text-start">Food pairing</th>
        <th scope="col"></th>
      </tr>
      <tr v-for="item in beerList" :key="item.id">
        <td><p class="text-start">{{ item.name }}</p></td>
        <td><p class="text-start">{{ item.first_brewed }}</p></td>
        <td><p class="text-start">{{ item.description }}</p></td>
        <td><p class="text-start">{{ item.food_pairing.toString()}}</p></td>
        <td><router-link :to="{ name: 'item', params: {id: item.id, name: item.name }}">Rate it!</router-link></td>
      </tr>
      </tbody>
    </table>
  </template>
</template>
<script>
/* eslint-disable */
import axios from 'axios';
import constants from "@/components/constants";

export default {
  data() {
    return {
      beerList: null
    };
  },
  methods: {
    async getApiData(searchTerm) {
      const headers = { "x-user": constants.API_EMAIL };
      const responce = await axios.get(constants.API_URL + '/beers/' + searchTerm, {headers});
      this.beerList = responce.data.data;
      console.log(responce.data.data);
    }
  }
};
</script>
