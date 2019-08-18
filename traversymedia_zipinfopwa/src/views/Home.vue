<template>
<!--
    1. Embeds components
    2. Retrieves info from API
    3. Sends info to ZipInfo.vue component for display
-->
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
//Tests are done by console.log(<your output>)

//retrieves components
import ZipSearch from "../components/ZipSearch";
import ZipInfo from "../components/ZipInfo";
import ClearInfo from "../components/ClearInfo";

export default {
  name: "home",
  //inserts components
  components: { ZipSearch, ZipInfo, ClearInfo },
  data(){
      return{
        info: null
      }
  },
  methods: {
    async getZipInfo(zip) {
    /*
        Async sends request to website
        Await fetches the response given i.e. data in JSON format
    */
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`);
      //If nothing was found i.e. 404 execute function 'showAlert'
      if (res.status == 404) {
        this.showAlert();
      }
      this.info = await res.json();
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Not Valid",
          message: "Please enter a valid US zipcode",
          buttons: ["OK"]
        })
        .then(a => a.present());
    },
    clearInfo(){
      this.info = null;
    }
    //for testing
    /* getZipInfo(zip){
          console.log(zip);
      } */
  }
};
</script>
