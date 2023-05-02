<template>
    <div class="card mx-auto p-0 m-1" style="width: auto;">
        <img v-bind:src="travelPost.imageUrl" class="card-image" alt="">
            <div class="travel-title">
                <h5 class="card-title">{{ travelPost.name }}</h5>
            </div>
        <div class="overlay-text">
            <p class="card-text">{{ travelPost.summary }}</p>
            <a href="#" class="btn btn-primary" v-on:click.prevent='goDetailPage(travelPost.id)'>Details</a>
        </div>
        <div class="overlay"></div>
    </div>
</template>

<script>

export default {
  name: 'HomeCard',
  props: ['travelPost'],
  methods: {
    goDetailPage (id) {
      this.$router.push({ path: `/travel/${id}` })
    }
  }
}
</script>

<style scoped>

.image {
  display: block;
  width: 100%;
  height: auto;
}

  .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: gray;
    overflow: hidden;
    width: 100%;
    height: 100%;
    opacity: 0;
    transition: opacity 0.5s;
  }

  .overlay-text {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-top: 50px;
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    overflow: hidden;
    width: 100%;
    height: 100%;
    opacity: 0;
    transition: opacity 0.5s;
    z-index: 1;
  }

  .travel-title {
    padding-top: 30px;
    position: absolute;
    width: 100%;
  }
  .travel-title h5 {
    background:  rgb(222, 223, 223, 0.5);
  }

  .card:hover .overlay {
    height: 100%;
    opacity: 0.5;
    transition: opacity 2s;
  }

  .card:hover .overlay-text {
    color: green;
    height: 100%;
    opacity: 1;
    transition: opacity 2s;
  }

.card-image {
  width: 250px;
  height: 400px;
}
</style>
