<template>
    <div>
      <input
        v-model="search"
        type="text"
        placeholder="Search contacts by name"
      />
      <button @click="showAddForm = !showAddForm">
        {{ showAddForm ? 'Cancel' : 'Add New Contact' }}
      </button>
      <ContactForm
        v-if="showAddForm"
        @submit="addContact"
        @cancel="cancelAddForm"
      />
      <ul>
        <li v-for="contact in filteredContacts" :key="contact.id">
          <router-link :to="'/contact/' + contact.id">
            {{ contact.firstName }} {{ contact.lastName }}
          </router-link>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import ContactForm from '../components/ContactForm.vue';
  
  export default {
    components: {
      ContactForm,
    },
    data() {
      return {
        contacts: JSON.parse(localStorage.getItem('contacts')) || [],
        search: '',
        showAddForm: false,
      };
    },
    computed: {
      filteredContacts() {
        return this.contacts
          .filter(
            (contact) =>
              contact.firstName.toLowerCase().includes(this.search.toLowerCase()) ||
              contact.lastName.toLowerCase().includes(this.search.toLowerCase())
          )
          .sort((a, b) => a.lastName.localeCompare(b.lastName));
      },
    },
    methods: {
      addContact(newContact) {
        newContact.id = Date.now();
        this.contacts.push(newContact);
        this.saveContacts();
        this.showAddForm = false;
      },
      cancelAddForm() {
        this.showAddForm = false;
      },
      saveContacts() {
        localStorage.setItem('contacts', JSON.stringify(this.contacts));
      },
    },
  };
  </script>
  
  <style scoped>
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    margin: 10px 0;
  }
  
  button {
    margin: 10px;
  }
  </style>
    