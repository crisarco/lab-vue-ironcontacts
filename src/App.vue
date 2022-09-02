<template>
  <h1>IronContacts</h1>
  <ContactsList/>
</template>

<script>
import ContactsList from "./components/ContactsList.vue";

export default {
  name: "App",
  components: { ContactsList }
}
</script>

<style>
body {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

h1 {
  font-size: 50px;
  text-align: center;
}
</style>
