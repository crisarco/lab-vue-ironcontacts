<template>
  <div class="buttons-container">
    <button>Add Random Contact</button>
    <button>Sort by popularity</button>
    <button>Sort by name</button>
  </div>
  <table v-if="fiveContacts.length" class="contacts-table">
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won Oscar</th>
      <th>Won Emmy</th>
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
      <td v-if="contact.wonOscar">
        Yes!!
      </td>
      <td v-else></td>
      <td v-if="contact.wonEmmy">
        Yes!!
      </td>
      <td v-else></td>
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

  .buttons-container {
    display: flex;
    justify-content: space-evenly;
  }

  .contacts-table {
    margin-top: 20px;
    text-align: center;
    width: 100%;
  }

  th {
    font-size: 20px;
  }

  td {
    font-size: 18px;
  }

</style>