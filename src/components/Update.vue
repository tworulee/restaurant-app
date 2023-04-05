<template>
  <Header />
  <h1>Hello User This is Update Restaurant Page</h1>
  <form class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter Name"
      v-model="restaurant.name"
    />
    <input
      type="text"
      name="Address"
      placeholder="Enter Address"
      v-model="restaurant.address"
    />
    <input
      type="Number"
      name="Contact"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
    />
    <button type="button" v-on:click="updateRestaurant">
      Update Restaurant
    </button>
  </form>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';
export default {
  name: 'AddRestaurant',
  components: {
    Header,
  },
  data() {
    return {
      restaurant: {
        name: '',
        address: '',
        contact: '',
      },
    };
  },
  methods: {
    async updateRestaurant() {
      console.log(this.restaurant);
      const result = await axios.put(
        'http://localhost:3000/restaurant/' + this.$route.params.id,
        {
          name: this.restaurant.name,
          address: this.restaurant.address,
          contact: this.restaurant.contact,
        }
      );
      if (result.status == 200) {
        this.$router.push({ name: 'HomePage' });
      }
    },
  },
  async mounted() {
    let user = localStorage.getItem('user-info');
    if (!user) {
      this.$router.push({ name: 'SignUp' });
    }
    let result = await axios.get(
      'http://localhost:3000/restaurant/' + this.$route.params.id
    );
    console.log(result);
    this.restaurant = result.data;
  },
};
</script>

<style></style>
