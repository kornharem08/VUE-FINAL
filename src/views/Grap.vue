<template>
<div><chartjs-doughnut v-bind:labels="labels" v-bind:datasets="datasets" v-bind:option="option"></chartjs-doughnut></div>
 
</template>

<script>    
import axios from 'axios'   
export default {
    data(){
        return{
            labels: [],
            datasets:[{
                data:[],
                backgroundColor:["Green","Yellow","Purple","Red","Cyan","Blue","Black","Gray","Blue","Aqua","AntiqueWhite","Gray","Blue","Aqua","AntiqueWhite"]
            }],
            option:{
                title:{
                    display:true,
                    position:"bottom",
                    text: "Fruits"
                }
            }
        };
    },
  mounted(){
      var instance = this
      axios
      .get('http://localhost:8080/api/supplier/CountCounty')
      .then(function(response){
for(var i=0;i<response.data.data.length;i++){
    console.log(response.data.data[i].country)
instance.labels.push(response.data.data[i].country)
instance.datasets[0].data.push(response.data.data[i].count)}
      })
  }
};
</script>