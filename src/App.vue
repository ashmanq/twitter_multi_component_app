<template lang="html">
  <section class="container">
    <div class="list">
      <h1>The Totally Not Twitter...Twitter</h1>
      <form v-on:submit.prevent="addTweet" class="list" action="index.html" method="post">
        <label for="name">Name</label>
        <input type="text" name="name" v-model:value="newTweet.name" required>
        <label for="handle">Handle</label>
        <input type="text" name="handle" v-model:value="newTweet.handle" required>
        <label for="tweet">Tweet</label>
        <input type="text" name="tweet" v-model:value="newTweet.tweet" required>
        <input class="btn" type="submit" name="submit" value="Add Tweet">
      </form>
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
      // We then add the new tweet to the list
      this.tweets.unshift(this.newTweet);
      // We then reset the form
      this.newTweet = {
        name:"",
        handle: "",
        tweet: ""
      };
    }
  },
  computed: {
    filterTweets: function() {
      return this.tweets.filter((tweet) => {
        return tweet.likes > 10;
      });

    }
  },
  components: {
    'twitter-tweet': Tweet
  }
}


</script>

<style lang="css" scoped>
h1 {
  text-align: center;
  font-size: 3em;
}

form {
  font-size: 1.2em;
  text-align: center;
  border-style: solid;
  border-color: #253341;
  border-radius: 5px;
  padding: 30px;
  color: #ffffff;
  background-color: #15202b;
}
label {
  padding: 10px;
}

input {
  font-size: 1.2em;
  text-align: center;
}

.btn {
  margin: 20px;
  padding:20px;
  border-style: none;
  background-color: #1da1f2;
  color: #ffffff;
  font-size: 1.2em;
  width:400px;
  align-self: center;
  border-radius: 5px;

}

.btn:hover {
  background-color:#197fbf;
}

.container {
  display:flex;
  height: 100%;
  align-self: center;
  justify-content: center;
  font-family: Roboto;
  font-size: 1em;
}

.list {
  display:flex;
  align-content: center;
  flex-direction: column;
}
</style>
