<template>
  <div>
    <h2>Add new friend</h2>
    <form @submit.prevent="addFriend">
      <label for="name">Name</label>
      <input type="text" name="name" v-model="addedContact.name" required/>
      <label for="phone">Phone</label>
      <input type="tel" name="phone" v-model="addedContact.phone" required />
      <label for="email">E-mail</label>
      <input type="email" name="email" v-model="addedContact.email" required/>
      <button>Add friend</button>
    </form>
  </div>
</template>

<script>
export default {
  emits: ["add-friend"],
  data() {
    return {
      addedContact: {
        name: "",
        phone: "",
        email: "",
      },
    };
  },
  methods: {
    addFriend() {
      this.$emit("add-friend", this.addedContact);
      this.addedContact.name = "";
      this.addedContact.phone = "";
      this.addedContact.email = "";
    },
  },
};
</script>

<style scoped>
</style>
