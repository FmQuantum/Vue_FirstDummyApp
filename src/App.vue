<template>
  <section>
    <header>
      <h1>My Friends</h1>
    </header>
    <add-friend @add-contact="addContact"></add-friend>
    <ul>
      <friend-contact v-for="friend in friends" :key="friend.id" :name="friend.name" :id="friend.id" :phone-number="friend.phone" :email-address="friend.email" :is-favorite="friend.isFavorite" @toggle-favorite="toggleFavStatus" @delete-friend="deleteFriend"></friend-contact>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return {
      friends: [
        {
          id: "manuel",
          name: "Manuel Lopez",
          phone: "0123 498 76 58",
          email: "manuel@localhost.com", 
          isFavorite: true
        },
        {
          id: "julie",
          name: "Julie Jones",
          phone: "0321 987 55 33",
          email: "julie@localhost.com",
          isFavorite: false 
        },
      ],
    };
  },
  methods: {
    toggleFavStatus(friendID) {
      // console.log("toggleFavStatus() triggered with ID: ", id)
      const identifiedFriend = this.friends.find(friend => friend.id === friendID);
      identifiedFriend.isFavorite = !identifiedFriend.isFavorite;
    },
    addContact(name, phone, email) {
      const newFriendConact = {
        id: new Date().toISOString(),
        name: name,
        phone: phone,
        email: email, 
        isFavorite: false
      }
      this.friends.push(newFriendConact);
    },
    deleteFriend(friendID) {
        const index = this.friends.findIndex(friend => friend.id === friendID);
        if (index !== -1) {
            this.friends.splice(index, 1);
        }
    },
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Jost&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Jost', sans-serif;
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
  form
{
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
