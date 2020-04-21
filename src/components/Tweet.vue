<template lang="html">
  <div class="row" v-bind:class="likedAlot" v-on:click="addLike">
      <img v-bind:class="likedAlot" v-bind:src="tweet.img" alt="Profile Pic">
      <div class="item">
        <h2>{{ tweet.handle }}</h2>
        <p>{{ tweet.tweet }}</p>
        <p>{{ tweet.name }}</p>
        <p> ❤️ {{ tweet.likes }}</p>
      </div>
  </div>
</template>

<script>
export default {
  name: 'tweet',
  props:['tweet'],
  methods: {
    // This method is used when a user clicks on a tweet. It
    // increments likes by 1 each time.
    addLike: function(){
      this.tweet.likes += 1;
    }
  },
  computed: {
    likedAlot: function() {
      return this.tweet.likes > 10 ? "really-liked" : "liked";
    }

  }
}
</script>

<style lang="css" scoped>
  img {
    height: 150px;
    width:150px;
    display:inline-block;
    border-style: solid;
    border-color: #253341;
    border-radius: 5px;
  }
  .row {
    display:flex;
    align-items: center;
    height:100%;
    padding: 30px;
    margin:10px;
    border-radius: 8px;
    border-style: solid;
    border-color: #38444d;
    color: #ffffff;
    background-color: #15202b;
  }
  .item {
    /* padding: 30px;
    margin:10px;
    border-radius: 8px; */
    font-size: 1.1em;
    padding-left: 30px;
    font-family: Roboto;

  }

  .really-liked {
    /* background-color: #ff2b2b; */
    border-color: #ff2b2b;
  }

  .liked {
    background-color: #15202b;
  }
</style>
