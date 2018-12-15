<template>
<div v-if="datasets[0].data.length >0">
    <chartjs-doughnut v-bind:labels="labels" v-bind:datasets="datasets" v-bind:option="option"></chartjs-doughnut></div>
 
</template>

<script>    
import axios from 'axios'   
export default {
    data(){
        return{
            labels: [],
            datasets:[{
                data:[],
                backgroundColor:['rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)',
                'rgba(300, 52, 75, 0.2)',
                'rgb(63, 191, 191)',
                'rgba(85, 63, 191, 0.67)',
                'rgba(63, 191, 148, 0.67)',
                'rgba(148, 63, 191, 0.67)',
                'rgba(54, 197, 226, 0.67)',
                'rgba(226, 114, 54, 0.67)',
                'rgba(54, 226, 140, 0.56)',
                'rgba(228, 5, 117, 0.87)',
                'rgba(133, 157, 239, 0.69)',
                'rgba(241, 79, 117, 0.78)']
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
      .get('https://evening-forest-72031.herokuapp.com/api/supplier/CountCounty')
      .then(function(response){
for(var i=0;i<response.data.data.length;i++){
    console.log(response.data.data[i].country)
instance.labels.push(response.data.data[i].country)
instance.datasets[0].data.push(response.data.data[i].count)}
      })
  }
};
</script>