<template>
<!--
    1. Searches values
    2. Confirms zipcode format
    3. Sends search value to Home.vue view component that sends API request
-->
    <ion-grid>
        <form @submit="onSubmit">
            <ion-col>
                <ion-item>
                <ion-label position="floating">Zipcode: </ion-label>
                    <ion-input :value="zip" @input="zip = $event.target.value" placeholder="Enter US Zipcode" name="zip">
                    </ion-input>
                </ion-item>
            </ion-col>
            <ion-col>
                <ion-button type="submit" color="primary" expand="block">Find</ion-button>
            </ion-col>
        </form>
    </ion-grid>
</template>

<script>
export default {
    name: "ZipSearch",
    data: function(){
        return{
            zip: ""
        }
    },
    methods: {
        onSubmit(e){
            //Prevents page from reloading after form submission
            e.preventDefault();
            //Zip Regex that verifies US zipcode
            const isValidZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
            //Test for valid zip
            if (! isValidZip) {
                this.showAlert();
                //Clear value
                this.zip = "";
            } else {
                this.$emit("get-zip", this.zip);
                //Clear value
                this.zip = "";
            }
        },
        showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Enter Zipcode",
                message: "Please enter a valid US zipcode",
                buttons: ["OK"]
            })
            .then(a => a.present());
        }
    }
}
</script>
