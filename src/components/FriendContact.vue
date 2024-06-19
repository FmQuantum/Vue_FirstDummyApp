<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="toogleIsFav"> Is Favorite</button>
    <button @click="toogleDetails">{{ detailsAreVisible ? 'Hide' : 'Show' }} Details</button>
    <ul v-if="detailsAreVisible">
      <li><strong>Phone: </strong>{{ phoneNumber }}</li>
      <li><strong>Email: </strong>{{ emailAddress }}</li>
    </ul>
    <button @click="deleteFriend">Delete</button>
  </li>
</template>

<script>
export default {
    // props: [
    //     'name',
    //     'phoneNumber',
    //     'emailAddress'
    // ],
    props: {
        id: {
            type: String,
            required: true
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
            type: Boolean,
            required: false,
            default: false,
            // validator: function(value) {
            //     return value === '1' || value === '0'
            // }
        },
    },
    emits: ['toggle-favorite', 'delete-friend'],
    //Below second way to define emit event with more details.
    // emits: {
    //     'toggle-favorite': function(id) {
    //         if (id) {
    //             return true;
    //         } else {
    //             console.warn("Id is missing!")
    //             return false;
    //         }
    //     },
    // },
    data() {
        return {
            detailsAreVisible: false,
        };
    },
    methods: {
        toogleDetails() {
        this.detailsAreVisible = !this.detailsAreVisible;
        },
        toogleIsFav() {
            // this.favoriteFriend = !this.favoriteFriend;
            this.$emit('toggle-favorite', this.id);

        },
        deleteFriend () {
            this.$emit('delete-friend', this.id)
            console.log("id:", this.id);
        },
    },

};
</script>
