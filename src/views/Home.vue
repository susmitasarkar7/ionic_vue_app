<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>ZipInfo</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch v-on:get-zip="getZipInfo" />
      <ZipInfo v-bind:info="info" />
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
import axios from "axios";

export default {
  name: 'home',
  components: {
    ZipSearch,
    ZipInfo  
  },
  data() {
    return {
      info: null,
      info1: null,
    }
  },
  methods: {
    async getZipInfo(zip) {
      // const res = await fetch(`http://api.zippopotam.us/IN/${zip}`); 
      // if(res.status == 404) {
      //   this.showAlert();
      // } 
      // const info = await res.json();
      // console.log(info);
      // this.info1 = await res.json().bind(this);
      // console.log(this.info1);
      
      axios.get(`http://api.zippopotam.us/IN/${zip}`)
      .then(function(res) {
        if(res.status == 404) {
          this.showAlert();
        }
        this.info = res.data;   
      }.bind(this))
      .catch()
      
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
            header: "Not Valid",
            message: "Please enter a valid Indian zipcode",
            buttons: ["OK"]
        })
        .then(a => a.present());
    }
  }
}
</script>
