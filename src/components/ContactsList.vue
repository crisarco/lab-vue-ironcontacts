<template>
  <table v-if="fiveContacts.length" class="contacts-table">
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
    </tr>
    <tr class="contact-list" v-for="contact in fiveContacts" :key="contact.id">
      <td>
        <img :src="`${contact.pictureUrl}`">
      </td>
      <td>
        {{ contact.name }}
      </td>
      <td>
        {{ contact.popularity }}
      </td>
    </tr>
  </table>
</template>

<script>
import contacts from "../contacts.json";

export default {
  name: 'ContactsList',
  data() {
    return {
      contactsData: contacts,
      fiveContacts: [],
    }
  },
  created() {
    for (let i = 0; i < 5; i++) {
      this.fiveContacts.push(this.contactsData.shift())
    }
  }
}
</script>

<style>
  img {
    width: 80px;
  }

</style>