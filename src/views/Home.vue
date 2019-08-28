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
      <ClearInfo v-bind:info="info" v-on:clear-info="clearInfo" />
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
import ClearInfo from "../components/ClearInfo";
import axios from "axios";

export default {
  name: 'home',
  components: {
    ZipSearch,
    ZipInfo,
    ClearInfo  
  },
  data() {
    return {
      info: null,
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
      
      axios.get(`http://api.zippopotam.us/IN/${zip}`)
      .then(function(res) {
        this.info = res.data;   
      }.bind(this))
      .catch(() => {
        this.showAlert();
      })
      
    },
    clearInfo() {
      // console.log('foo');
      
      this.info = null;
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
