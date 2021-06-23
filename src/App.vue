<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <add-friend @add-friend="addFriend"/>
  <ul class="contacts_list">
    <friend-contacts
      v-for="friend in friends"
      :key="friend.id"
      :id="friend.id"
      :name="friend.name"
      :phone="friend.phone"
      :email="friend.email"
      :avatarShown="friend.avatarShown"
      @show-avatar="showFriendAvatar"
      @delete-friend="deleteFriend"
    />
  </ul>
</template>

<script>
import FriendContacts from "./components/FriendContacts.vue";
import AddFriend from "./components/AddFriend.vue";

export default {
  name: "App",
  components: {
    FriendContacts,
    AddFriend,
  },
  data() {
    return {
      friends: [
        {
          id: "manuel",
          name: "Manuel Lorenz",
          phone: "0123 45678 90",
          email: "manuel@localhost.com",
          avatarShown: false,
        },
        {
          id: "julie",
          name: "Julie Jones",
          phone: "4952 22304 12",
          email: "julie@localhost.com",
          avatarShown: false,
        },
      ],
    };
  },
  methods: {
    showFriendAvatar(id) {
      const identifiedFriend = this.friends.find(friend => friend.id === id);
      identifiedFriend.avatarShown = !identifiedFriend.avatarShown;
    },
    addFriend(friend) {
      const newFriend = {
        id: new Date().toISOString(),
        name: friend.name,
        phone: friend.phone,
        email: friend.email,
        avatarShown: false,
      };
      this.friends.push(newFriend);
    },
    deleteFriend(id) {
      this.friends = this.friends.filter(friend => friend.id !== id);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.contacts_list,
.contacts_list li {
  list-style-type: none;
}
</style>
