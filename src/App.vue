<template>
 <!-- Button trigger modal -->
 
  <h1>รายการปล่อยจรวดทั้งหมด</h1>
  <div class="p-4" id="app" >
    <table class="table table-bordered table-dark">
      <thead>
            <tr>
                <th >ลำดับ</th>
                <th >ชื่อ</th>
                <th >เวลาปล่อย</th>
                <th >รูปภาพประกอบ</th>
                <th >จำนวน crew</th>
            </tr>
        </thead>
      <TableShowLaunch v-for="(launch,index) in launches"
      :key="index"
      :no="index"
      :name="launch.name"
      :date="launch.date_local"
      :pict="launch.links.flickr.original"
      :crew="launch.crew"
      @detail="getDetail"
      />
     </table>
    </div>

    <TheModal :detail="detail" 
    :pict="pict"/>
   
  
</template>

<script>
//importing bootstrap 5
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap/dist/js/bootstrap.min.js";

import axios from 'axios'

import TableShowLaunch from './components/TableShowLaunch.vue';
import TheModal from './components/TheModal.vue';
export default {
  name: "App",
  components: {
    TableShowLaunch,
    TheModal,
  },
  data(){
    return{
      launches: [],
      detail:[],
      pict:"",
    }
  },
  methods: {
    getLaunch() {
      const URL = "https://api.spacexdata.com/v5/launches/";
      axios.get(URL).then(res => {
          console.log(res.data);
          this.launches = res.data;
        })
    },
    getDetail(id){
        console.log("Detail of ID:"+id);  
        var URL = "https://api.spacexdata.com/v5/launches/";
        axios.get(URL).then(res => {
            this.detail = res.data[id];
            this.pict = res.data[id].links.flickr.original;

        })
        // // console.log("Rocket");
        // // //console.log(this.rocket_id)
        // // URL = "https://api.spacexdata.com/v4/rockets";
        // // axios.get(URL).then(res => {
          
        // //   if(res.data.id ==  this.rocket_id)
        // //       console.log(res.data.id);
        // //    this.rocket = res.data;
        // //    // console.log(this.rocket.name)
        // //   })

        // URL = "https://api.spacexdata.com/v4/launchpads";
        // axios.get(URL).then(res => {
        //     res.data.forEach(function(element){
        //       //console.log(element.id);
        //       if(element.id === launchpad_id){
        //         console.log("ID:"+element.id+"Name:"+element.name);
        //         this.launchpad = res.data;
        //       }
        //     });
        // })
        
        // // URL = "https://api.spacexdata.com/v4/crew";
        // // axios.get(URL).then(res => {
        // //     this.launchpad = res.data;
        // //   })
    }

  },
  mounted() {
    this.getLaunch();
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
