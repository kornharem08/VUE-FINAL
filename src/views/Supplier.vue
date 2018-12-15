<template>
  <div>
      <div id="tophead"> <h2>Supplier List</h2></div>
   
     <b-row>
      <b-col md="3" class="my-1">
        <b-form-group horizontal label="Search" class="mb-0">
          <b-input-group>
            <b-form-input v-model="filter" placeholder="Type to Search" />
            <b-input-group-append>
              <b-btn :disabled="!filter" @click="filter = ''">Clear</b-btn>
            </b-input-group-append>
          </b-input-group>
        </b-form-group>
      </b-col>
       </b-row>
       
    <b-table striped hover :items="supplier" :fields="fields" :per-page="pageSize" :current-page="pageIndex"  :filter="filter">
         <template slot="show_details" slot-scope="row">
      <!-- we use @click.stop here to prevent emitting of a 'row-clicked' event  -->
      <b-button size="sm" @click.stop="row.toggleDetails" class="mr-2">
       {{ row.detailsShowing ? 'Hide' : 'Show'}} Details
      </b-button>
      <!-- In some circumstances you may need to use @click.native.stop instead -->
      <!-- As row.showDetails is one-way, we call the toggleDetails function on @change -->
     
    </template>
    <template slot="row-details" slot-scope="row">
      <b-card>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Supplier_id:</b></b-col>
          <b-col>{{ row.item.supplier_id }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Companyname:</b></b-col>
          <b-col>{{ row.item.company_name }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Contact_name:</b></b-col>
          <b-col>{{ row.item.contact_name }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Contact_title:</b></b-col>
          <b-col>{{ row.item.contact_title }}</b-col>
        </b-row>
         <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Address:</b></b-col>
          <b-col>{{ row.item.address }}</b-col>
        </b-row>
         <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>City:</b></b-col>
          <b-col>{{ row.item.city }}</b-col>
        </b-row>
         <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Region:</b></b-col>
          <b-col>{{ row.item.region }}</b-col>
        </b-row>
         <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Postal_code:</b></b-col>
          <b-col>{{ row.item.postal_code }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Fax:</b></b-col>
          <b-col>{{ row.item.fax }}</b-col>
        </b-row>
        <b-row class="mb-2">
          <b-col sm="3" class="text-sm-right"><b>Homepage:</b></b-col>
          <b-col>{{ row.item.homepage }}</b-col>
        </b-row>
       
        <b-button size="sm" @click="row.toggleDetails">Hide Details</b-button>
      </b-card>
    </template>
    </b-table>
    <b-pagination align="center" size="lg" :total-rows="supplier" v-model="pageIndex" :per-page="pageSize">
    </b-pagination>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'supplier',
  components: {
    
  },
  data(){
      return{
          message: 'Project22'
      }
  },
   data(){
      return{
          message: 'Project2',
          supplier: [],
          pageSize: 10,
          pageIndex:1,
          filter: null,
           fields: [ 
               {
                   key:'supplier_id',
                   sortable :true,
                   
               },
               {
                    key:'company_name',
                   sortable :true
               },
              
               {
                    key:'phone',
                   sortable :true,
           
               },
                {
                    key:'country',
                   sortable :true,
                 
               },
                 {
          key:  'show_details'  
        }     
               ],
      }
      
  },
   computed: {
    sortOptions () {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => { return { text: f.label, value: f.key } })
    }
  },
  mounted(){
      var instance = this
      axios
      .get('https://evening-forest-72031.herokuapp.com/api/supplier')
      .then(function(response){
console.log(response.data)
instance.supplier =response.data.data
      })
  }
}
</script>

<style>
#tophead{
    margin-top: 30px;
}
h2{
    margin-top: 50px;
}
</style>
