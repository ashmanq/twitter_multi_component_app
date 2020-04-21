<template lang="html">
  <section class="container">

    <h1>The Totally Not Twit... Tweeting App</h1>

    <div class="list">

      <form v-on:submit.prevent="addTweet" class="list" action="index.html" method="post">
        <label for="name">Name</label>
        <input type="text" name="name" v-model:value="newTweet.name" required>
        <label for="handle">Handle</label>
        <input type="text" name="handle" v-model:value="newTweet.handle" required>
        <label for="tweet">Tweet</label>
        <input type="text" name="tweet" v-model:value="newTweet.tweet" autocomplete="off" required>
        <input class="btn" type="submit" name="submit" value="Add Tweet">
        <button type="button" class="btn" v-on:click="filterTweets" name="filter" >View Liked Tweets</button>
      </form>
    </div>
    <div class="list">

      <twitter-tweet v-for="(tweet,index) in tweets" :key="index" :tweet="tweet">
      </twitter-tweet>

    </div>
  </section>
</template>

<script>
import Tweet from './components/Tweet.vue';

export default {
  name: 'app',
  data() {
    return {
      tweets:[
        {
          id: 1,
          name: 'James',
          handle: '@jokerjames',
          img: 'https://semantic-ui.com/images/avatar2/large/matthew.png',
          tweet: "If you don't succeed, dust yourself off and try again.",
          likes: 10,
        },
        {
          id: 2,
          name: 'Fatima',
          handle: '@fantasticfatima',
          img: 'https://semantic-ui.com/images/avatar2/large/molly.png',
          tweet: 'Better late than never but never late is better.',
          likes: 12,
        },
        {
          id: 3,
          name: 'Xin',
          handle: '@xeroxin',
          img: 'https://semantic-ui.com/images/avatar2/large/elyse.png',
          tweet: 'Beauty in the struggle, ugliness in the success.',
          likes: 18,
        }
      ],
      newTweet: {
        id: 0,
        name: "",
        handle: "",
        img: 'https://semantic-ui.com/images/avatar2/large/matthew.png',
        tweet: "",
        likes: 0
      }
    }
  },
  methods: {
    addTweet: function() {
      // To allocate id number we look at size of array and add 1.
      this.newTweet.id = this.tweets.length + 1;
      // We check to see if handle has an @ sign at the beginning. If not
      // then we manually add one.
      if(!this.newTweet.handle.startsWith('@')){
        this.newTweet.handle = '@' + this.newTweet.handle;
      }
      // We then add the new tweet to the list
      this.tweets.unshift(this.newTweet);
      // We then reset the form
      this.newTweet = {
        id:0,
        name:"",
        handle: "",
        img: 'https://semantic-ui.com/images/avatar2/large/matthew.png',
        tweet: "",
        likes: 0
      };
    }
  },
  methods: {
    filterTweets: function() {
      const likedTweets = this.tweets.filter((tweet) => {
        return tweet.likes > 10;
      });
      console.log(likedTweets);
    }
  },
  components: {
    'twitter-tweet': Tweet
  }
}


</script>
<!-- I've created this unscoped style to colour the background
all one colour -->
<style media="screen">
body{
  background-color: #15202b;
}
</style>
<style lang="css" scoped>


h1 {
  text-align: center;
  margin: 40px;
  font-size: 3rem;
  color: #1da1f2;
}

form {
  /* width:300px; */
  font-size: 1.2rem;
  text-align: center;
  border-style: solid;
  border-color: #253341;
  border-radius: 8px;
  padding: 30px;
  margin:10px;
  color: #ffffff;
  background-color: #15202b;
}
label {
  font-size: 1.2rem;
  padding: 10px;

}

input {
  font-size: 1.2rem;
  text-align: center;
  padding:10px;
  margin-bottom: 20px;
  border-style: solid;
  border-color: #15202b;
  border-radius: 5px;
}

.btn {
  margin: 20px;
  padding:10px;
  border-style: none;
  background-color: #1da1f2;
  color: #ffffff;
  font-size: 1.2em;
  width:200px;
  align-self: center;
  border-radius: 5px;

}

.btn:hover {
  background-color:#197fbf;
}

.container {
  display:flex;
  flex-direction: column;
  justify-content: center;
  /* align-self: center; */
  width: auto;
  align-content: center;
  align-items: center;
  font-family: Roboto;
  font-size: 1em;
}

.list {
  display:flex;
  align-content: center;
  justify-content: center;
  flex-direction: column;

}
</style>
