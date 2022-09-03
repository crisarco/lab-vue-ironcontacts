<template>
  <div class="buttons-container">
    <button @click="getRandomElem">Add Random Contact</button>
    <button @click="sortByPopularity">Sort by popularity</button>
    <button @click="sortByName">Sort by name</button>
  </div>
  <table v-if="fiveContacts.length" class="contacts-table">
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won Oscar</th>
      <th>Won Emmy</th>
      <th>Actions</th>
    </tr>
    <tr class="contact-list" v-for="contact in fiveContacts" :key="contact.id">
      <td>
        <img :src="`${contact.pictureUrl}`">
      </td>
      <td>
        {{ contact.name }}
      </td>
      <td>
        {{ contact.popularity ? contact.popularity.toFixed(2) : 0 }}
      </td>
      <td>
        <img v-if="contact.wonOscar" src="../assets/trofeo.png">
      </td>
      <td>
        <img v-if="contact.wonEmmy" src="../assets/trofeo.png">
      </td>
      <td><button @click="deleteContact(contact.id)">Delete</button></td>
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
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min) + min); 
    },
    getRandomElem() {
      if (this.contactsData.length) {
        const myRandomPos = this.getRandomInt(0, this.contactsData.length - 1);
        const myRandomElem = this.contactsData[myRandomPos];
        const elemIsAvailableToShow = this.fiveContacts.findIndex(elem => elem === myRandomElem);

        if (elemIsAvailableToShow === -1) {
          this.fiveContacts.push(myRandomElem);
          const elemToRemoveIndex = this.contactsData.findIndex(elem => elem === myRandomElem);
          this.contactsData.splice(elemToRemoveIndex, 1);
        }
      }
    },
    sortByName() {
      this.fiveContacts.sort((a,b) => a.name > b.name ? 1 : -1);
    },
    sortByPopularity() {
      this.fiveContacts.sort((a,b) => b.popularity - a.popularity);
    },
    deleteContact(contactId) {
      const contactIndexFound = this.fiveContacts.findIndex(elem => elem.id === contactId);
      if (contactIndexFound !== -1) {
        this.contactsData.push(this.fiveContacts.splice(contactIndexFound,1)[0]);
      }
    }
   },
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