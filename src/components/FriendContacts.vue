<template>
  <li>
    <h2>{{ name }}</h2>
    <img src="" :alt="name + `'s avatar`" v-show="avatarShown" />
    <button @click="showAvatar">
      {{ avatarShown ? "Hide" : "Show" }} Avatar
    </button>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phone }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ email }}
      </li>
    </ul>
    <button @click="deleteFriend">Delete friend</button>
  </li>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    phone: {
      type: String,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    avatarShown: {
      type: Boolean,
      required: true,
    },
    id: {
      type: String,
      required: true,
    },
  },
  emits: ["show-avatar", "delete-friend"],
  data() {
    return {
      detailsAreVisible: false,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    showAvatar() {
      this.$emit("show-avatar", this.id);
    },
    deleteFriend() {
      if (!confirm("Are you sure you want to delete this friend?")) {
        console.log("You denied deleting friend.");
      } else {
        this.$emit("delete-friend", this.id);
      }
    },
  },
};
</script>
