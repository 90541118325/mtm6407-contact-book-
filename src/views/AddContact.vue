<template>
  <div>
    <h2>Add New Contact</h2>
    <form @submit.prevent="addContact">
      <input v-model="firstName" type="text" placeholder="First Name" required />
      <input v-model="lastName" type="text" placeholder="Last Name" required />
      <input v-model="email" type="email" placeholder="Email" required />
      <input v-model="phone" type="text" placeholder="Phone" required />
      <button type="submit">Save</button>
    </form>
    <button @click="goBack">Cancel</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      firstName: '',
      lastName: '',
      email: '',
      phone: '',
    };
  },
  methods: {
    addContact() {
      const newContact = {
        id: Date.now().toString(),
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
        phone: this.phone,
      };
      const contacts = JSON.parse(localStorage.getItem('contacts')) || [];
      contacts.push(newContact);
      localStorage.setItem('contacts', JSON.stringify(contacts));
      this.$router.push(`/contact/${newContact.id}`);
    },
    goBack() {
      this.$router.push('/');
    },
  },
};
</script>
