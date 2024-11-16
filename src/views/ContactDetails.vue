<template>
  <div>
    <h2>{{ contact.firstName }} {{ contact.lastName }}</h2>
    <p><strong>Email:</strong> {{ contact.email }}</p>
    <p><strong>Phone:</strong> {{ contact.phone }}</p>
    <button @click="goToEdit">Edit</button>
    <button @click="deleteContact">Delete</button>
    <button @click="goBack">Back to List</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      contact: {},
    };
  },
  mounted() {
    const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
    this.contact = contacts.find(
      (contact) => contact.id === this.$route.params.id
    );
  },
  methods: {
    goToEdit() {
      this.$router.push(`/edit/${this.contact.id}`);
    },
    deleteContact() {
      const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      const updatedContacts = contacts.filter(
        (c) => c.id !== this.contact.id
      );
      localStorage.setItem('contacts', JSON.stringify(updatedContacts));
      this.$router.push('/');
    },
    goBack() {
      this.$router.push('/');
    },
  },
};
</script>
