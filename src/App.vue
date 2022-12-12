<template>
  <section>
    <header>
      <h1>My Friends List</h1>
    </header>
    <!--Add a new friend component -->
    <new-friend @add-contact="addContact"></new-friend>
    <ul>
      <li>
        <ul>
          <!---Friend contact component with props: static values
          <friend-contact
            name="Manuel Lorenz" phone-number="01234 78992"
            email-address="manuel@localhost.com" v-bind:is-favorite="true"
            >
          </friend-contact>
          <friend-contact
            name="Julie Jones" phone-number="0987 65431"
            email-address="julie@localhost.com" 
            >
          </friend-contact> -->
          <!--Friend contact component with props: dynamic values -->
          <!-- Add the emit listener toggle-favorite with an on-click as a prop for friend-contact. 
          It should call a method to toggle the favorite status -->
          <!--ID Prop for each friend-contact. id prop should be equivalent to the key of each element-->
          <!--Make sure to define the id prop first before any other prop -->
          <friend-contact
            v-for="friend in friends"
            :id="friend.id"
            :key="friend.id"
            :name="friend.name"
            :phone-number="friend.phoneNumber"
            :email-address="friend.emailAddress"
            :is-favorite="friend.isFavorite"
            @toggle-favorite="toggleFavoriteStatus"
            @deleteFriend="deleteContact"
          >
          </friend-contact>
        </ul>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      //The data from the FriendContact component is moved here to its' parent app
      friends: [
        {
          id: "manuel",
          name: "Manuel Lorenzo",
          phoneNumber: "0123 456 7890",
          emailAddress: "manuel@localhost.com",
          isFavorite: true,
        },
        {
          id: "julie",
          name: "Julie Jones",
          phoneNumber: "123 245 6789",
          emailAddress: "julie@localhost.com",
          isFavorite: false,
        },
      ],
    };
  },
  methods: {
    //Toggle method
    toggleFavoriteStatus(friendId) {
      // alert("This Works!");
      console.log(friendId);
      //Searches friends array for friend with the same ID
      const identifiedFriend = this.friends.find(
        (friend) => friend.id === friendId
      );
      console.log(identifiedFriend);
      identifiedFriend.isFavorite = !identifiedFriend.isFavorite;
    },
    //Add Contact from Form
    addContact(name, phone, email) {
      const newFriend = {
        id: new Date().toISOString(), //using a timestamp as the unique id for each friend
        name: name,
        phoneNumber: phone,
        emailAddress: email,
        isFavorite: false
      };
      this.friends.push(newFriend); //push new friend to friends array
    },
    deleteContact(friendID) {
    //Return an array without the friend with this friendID using Array.filter method
      this.friends = this.friends.filter(
        (friend) => friend.id != friendID //If they are not equal, return false. Otherwise, return true.
      ) 
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Jost&display=swap");
* {
  box-sizing: border-box;
}

html {
  font-family: "Jost", sans-serif;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

#app li,
#app form {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}

#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}
</style>