<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>Deck complet</h3>
    <ul>
      <li v-for="item in deck" :key="item.id">{{ item.number }}{{ item.sign }}</li>
    </ul>
    <button @click="picker">Pick a card!</button>
    <h3>Card</h3>
    <p>{{card.number}}{{card.sign}}</p>
    <img width="15%" :src="getImgUrl(card.png)" v-bind:alt="card.number">
  </div>
</template>

<script>
import Deck from "./../deck.json";
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      deck: Deck,
      card: ""
    };
  },
  methods: {
    picker: function() {
      var chosenNumber = Math.floor(Math.random() * this.deck.length);
      this.card = this.deck[chosenNumber];
      console.log(this.card);
    },
    getImgUrl(imageName) {
      console.log(imageName);
      if (imageName !== undefined) {
        return require("./../assets/" + imageName);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
