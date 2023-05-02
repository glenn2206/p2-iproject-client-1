<template>
<div class="section p-2 vh-80" style='background-color: #FFDEE9;
        background-image: linear-gradient(0deg, #FFDEE9 0%, #B5FFFC 100%);
        '>
        <h1 class="bg-secondary">Our Travel Pack</h1>
        <div class="container">

          <HomeCardVue v-for="travelPost in travelPosts" v-bind:key='travelPost.id' v-bind:travelPost='travelPost' />

        </div>
        <h1 class="bg-secondary">Your Booking</h1>
        <div class="container" v-if="role === 'customer'">
            <div class="card mx-auto m-1" style="width: 18rem;" v-for="booking in bookings" v-bind:key='booking.id'>
              <img v-bind:src="booking.TravelPost.imageUrl" class="card-img-top" alt="">
              <div class="card-body">
                <h5 class="card-title">{{ booking.TravelPost.name }}</h5>
                <p class="card-text">{{ booking.TravelPost.summary }}</p>
                <a href="#" class="btn btn-primary" v-on:click.prevent='goDetailPage(booking.TravelPost.id)'>Details</a>
              </div>
            </div>
        </div>
        <ChatRoomVue />

</div>
</template>

<script>
import ChatRoomVue from '../components/ChatRoom.vue'
import HomeCardVue from '../components/HomeCard.vue'

export default {
  name: 'Home',
  components: { HomeCardVue, ChatRoomVue },
  data () {
    return {
      email: localStorage.getItem('email')
    }
  },
  created () {
    this.$store.dispatch('refresh')
    this.$store.dispatch('fetchTravels')
    this.$store.dispatch('fetchBookings')
    this.$store.dispatch('forRefresh')
  },
  computed: {
    role () {
      return this.$store.state.role
    },
    travelPosts () {
      return this.$store.state.travelPosts
    },
    bookings () {
      return this.$store.state.bookings
    }
  }
}
</script>

<style scoped>
  body {
    margin: 20px auto;
    font-family: "Lato";
    font-weight: 300;
  }input {
    font-family: "Lato";
  }a {
    color: #0000ff;
    text-decoration: none;
  }a:hover {
    text-decoration: underline;
  }#wrapper,
  #loginform {
    margin: 0 auto;
    padding-bottom: 25px;
    background: #eee;
    max-width: 100%;
    border: 2px solid #212121;
    border-radius: 4px;
  }
  #name {
    border-radius: 4px;
    border: 1px solid #ff9800;
    padding: 2px 8px;
  }
  #submitmsg,
  #enter{
    background: #ff9800;
    border: 2px solid #e65100;
    color: white;
    padding: 4px 10px;
    font-weight: bold;
    border-radius: 4px;
  }
  #menu {
    padding: 15px 25px;
    display: flex;
  }
  #menu p.welcome {
    flex: 1;
  }
  a#exit {
    color: white;
    background: #c62828;
    padding: 4px 8px;
    border-radius: 4px;
    font-weight: bold;
  }
  .msgln {
    margin: 0 0 5px 0;
  }
  .msgln span.left-info {
    color: orangered;
  }
  .msgln span.chat-time {
    color: #666;
    font-size: 60%;
    vertical-align: super;
  }
  .msgln b.user-name, .msgln b.user-name-left {
    font-weight: bold;
    background: #546e7a;
    color: white;
    padding: 2px 4px;
    font-size: 90%;
    border-radius: 4px;
    margin: 0 5px 0 0;
  }
  .msgln b.user-name-left {
    background: orangered;
  }
  .container {
    display: flex;
    flex-wrap: wrap;
  }
</style>
