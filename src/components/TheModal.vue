<template>
  <div class="container p-5">
    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title text-info" id="exampleModalLabel">รายละเอียด</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <h1>ข้อมูลเพิ่มเติม</h1>
            <img :src="pict" alt="" width="250" height="250" v-if="pict != '' " >
            <img src="https://static.thenounproject.com/png/3674270-200.png"  width="250" height="250" v-else>
           
            <h3>ชื่อจรวด:{{detail.name}}</h3>
            <h3>ฐานยิง :{{detail.launchpad}}</h3>
            <h3>คำอธิบาย :{{detail.details}}</h3>
            <h3>จำนวนนักบิน :{{detail.crew}}</h3>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-warning" data-bs-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap/dist/js/bootstrap.min.js";
import axios from 'axios'
export default {
    name:"TheModal",
    props: ["detail","pict"],
    data(){
        return{
        launche_id: 0,
        rocket_id:0,
        lp_name:"",
        }
    },
    methods: {
        getLaunchpad(id) {
            var URL = "https://api.spacexdata.com/v4/launchpads?id="+id;
            //console.log(URL)
            this.lp_name =  axios.get(URL).then(res => {
                res.data.forEach(function(element){
                //console.log(element.id);
                if(element.id === id){
                    //console.log("ID:"+element.id+"Name:"+element.name);
                    return element.name;
                }
                });
            })
        },
    }
}
</script>

<style>

</style>