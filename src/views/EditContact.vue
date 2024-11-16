<template>
  <div>
    <h2>Edit Contact</h2>
    <form @submit.prevent="editContact">
      <input v-model="contact.firstName" type="text" required />
      <input v-model="contact.lastName" type="text" required />
      <input v-model="contact.email" type="email" required />
      <input v-model="contact.phone" type="text" required />
      <button type="submit">Save Changes</button>
    </form>
    <button @click="goBack">Cancel</button>
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
    editContact() {
      const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      const updatedContacts = contacts.map((c) =>
        c.id === this.contact.id ? this.contact : c
      );
      localStorage.setItem('contacts', JSON.stringify(updatedContacts));
      this.$router.push(`/contact/${this.contact.id}`);
    },
    goBack() {
      this.$router.push('/');
    },
  },
};
</script>
