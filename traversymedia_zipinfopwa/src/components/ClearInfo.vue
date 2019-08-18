<template>
<!--
    Clears info retrived by setting it to null
    in the HOme.vue view component
-->
<ion-button color="light" expand="block" @click="$emit('clear-info')"  v-if="info">
    Clear
</ion-button>
</template>

<script>
export default {
    name: "ClearInfo",
    props: ["info"]
}
</script>
