<template>
  <li>
    <h2>{{ isFavorite ? "(Favorite)" : "" }} {{ name }}</h2>
    <button v-on:click="toggleDetails">
      {{ detailsAreVisible ? "Hide" : "Show" }} Details
    </button>
    <!--- Toggle Favorite Button: Checks if friendIsFavorite is true or false--->
    <!--This on-click can be removed, we can use an Emit Listener 
    on <friend-contact> in App.Vue instead
    <button v-on:click="toggleFavorite">-->

    <button v-on:click="toggleFavorite">
      {{ isFavorite ? "Unmark Favorite" : "Mark Favorite" }}
    </button>
    <ul v-if="detailsAreVisible">
      <!--<li><strong>ID: </strong> {{ id }}</li> -->
      <li><strong>Phone: </strong> {{ phoneNumber }}</li>
      <li><strong>Email: </strong> {{ emailAddress }}</li>
    </ul>
    <button @click="$emit('deleteFriend', id)">Delete Contact</button>
  </li>
</template>

<script>
export default {
  emits: {
    //Include the Emit Identifier and a Validation Function.
    //The Validation Function checks if all the props in the Emit is truthy/exists.
    //Otherwise return an error to warn developers
    "toggle-favorite": function (id) {
      if (id) {
        return true;
      } else {
        console.warn("ID is missing!");
        return false;
      }
    },
    "deleteFriend": {}
  },
  //Four Props to use as parameters
  props: {
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: String,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean, //Validator function not neccessary if type is boolean
      //validator: function(value) {
      //	return value === '1' || value === "0",
      //}
      required: false, //not required for friend component
      default: false, //has a default value of false
    },
  },
  data() {
    return {
      //Reference data property to favorite prop (used for mutation)
      //Using this reference data property is now unneccessary
      //friendIsFavorite: this.isFavorite,
      detailsAreVisible: false,
      //This can now be commented out (not using this data. We are using App.Vue's data)
      // friend: {
      // id: "manuel",
      //   name: "Manuel Lorenz",
      //   phone: "0123 45678 90",
      //   email: "manuel@localhost.com",
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      //if (this.friendIsFavorite === '1') {
      //    this.friendIsFavorite = "0"
      //} else {
      //    this.friendIsFavorite = "1"
      //}
      //Updates for use with boolean data type:
      //this.friendIsFavorite = !this.friendIsFavorite;
      //Emit Event Listener
      //toggleFavorite should now be an Event/Emit Listener, not a method
      this.$emit("toggle-favorite", this.id);
    }
  },
};
</script>
<style>
#app input {
  font: inherit;
  padding: 0.15rem;
}
#app label {
  font-weight: bold;
  margin-right: 1rem;
  width: 7rem;
  display: inline-block;
}
#app form div {
  margin: 1rem 0;
}
</style>