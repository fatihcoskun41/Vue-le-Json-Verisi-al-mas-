<template>
<div>
<h2>{{title}}</h2>
<div class="input-group rounded search w-50 p-5 m-auto">
  <input v-model="search" type="search" class="form-control rounded" placeholder="Search" aria-label="Search"
    aria-describedby="search-addon" />



</div>

  <div v-if="search.length>0" class="alert alert-success w-50 m-auto" role="alert">
    <span>Şuanki Aramanız : {{search}}</span>

  </div>


<table class="table ">
  <thead>
    <tr>
      <th scope="col">Country</th>
      <th scope="col">Capital</th>
      <th scope="col">Region</th>
      <th scope="col">Flag</th>
    </tr>
  </thead>
  <tbody>

    <tr v-for="i in filteredwithAllPropertyPosts"  :key="i.numericCode">

      <td style="width:25%">{{i.name}}</td>
      <td style="width:25%">{{i.capital}}</td>
      <td style="width:25%">{{i.region}}</td>
      <td style="width:25%"><img  width="50%" :src="i.flag" class="img-thumbnail" alt="..."></td>
    </tr>



    
  </tbody>
</table>
</div>
  
</template>

<script>
import Vue from 'vue';

import axios from 'axios';
import VueAxios from 'vue-axios'
Vue.use(VueAxios,axios)
export default {
  components: {

  },
    data() {
        return {
            title:"Countries",
            list:[],
            search:'',

            
        }
    },
    mounted() {
        Vue.axios.get('https://restcountries.eu/rest/v2/all')
        .then((response)=>{
            this.list=response.data
        })
    },
  computed: {
    filteredwithCapitalPosts(){
     return this.list.filter(post => post.capital.toLowerCase().includes(this.search.toLowerCase()))
      // capitala göre sıralama
    },
    filteredwithAllPropertyPosts(){
      return this.list.filter(post=>
          post.name.toLowerCase().includes(this.search.toLowerCase()) || post.capital.toLowerCase().includes(this.search.toLowerCase()) || post.region.toLowerCase().includes(this.search.toLowerCase())
          //tüm değerlere göre sıralama
      )
    }

  },
  
   
    

}
</script>

<style>

</style>
