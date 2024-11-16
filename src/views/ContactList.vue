<template>
  <div>
    <h1>Contact Book</h1>
    <input
      v-model="searchQuery"
      type="text"
      placeholder="Search by name"
      class="search-bar"
    />
    <ul>
      <li
        v-for="contact in filteredContacts"
        :key="contact.id"
        @click="goToDetails(contact.id)"
        class="contact-item"
      >
        {{ contact.lastName }}, {{ contact.firstName }}
      </li>
    </ul>
    <button @click="goToAddContact" class="add-btn">Add New Contact</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      contacts: JSON.parse(localStorage.getItem('contacts')) || [],
      searchQuery: '',
    };
  },
  computed: {
    filteredContacts() {
      return this.contacts
        .filter((contact) =>
          `${contact.firstName} ${contact.lastName}`
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase())
        )
        .sort((a, b) => a.lastName.localeCompare(b.lastName));
    },
  },
  methods: {
    goToDetails(id) {
      this.$router.push(`/contact/${id}`);
    },
    goToAddContact() {
      this.$router.push('/add');
    },
  },
};
</script>
