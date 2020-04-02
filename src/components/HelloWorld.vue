<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h3>Joueur</h3>
    <ul v-for="person in persons" :key="person.id">
      <li>{{ person.name }}</li>
      <li>{{ person.status }}</li>
      <li v-for="personCard in person.cards" :key="personCard.id">
        <img width="15%" :src="getImgUrl(personCard.png)" v-bind:alt="personCard.number">
      </li>
    </ul>
    <h3>Deck complet</h3>
    <ul>
      <li v-for="item in deck" :key="item.id">{{ item.number }}{{ item.sign }}</li>
    </ul>
    <button @click="pickACard">Pick a card!</button>
    <h3>Card</h3>
    <p>{{card.number}}{{card.sign}}</p>
    <img width="15%" :src="getImgUrl(card.png)" v-bind:alt="card.number">
  </div>
</template>

<script>
/* eslint-disable */
import Deck from "./../deck.json";
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      deck: Deck,
      card: "",
      round: 0,
      persons: [
        {
          id: 0,
          name: "Robert",
          status: "Joue",
          cards: []
        },
        {
          id: 1,
          name: "Kévin",
          status: "En attente",
          cards: []
        }
      ]
    };
  },
  methods: {
    pick: function() {
      var chosenNumber = Math.floor(Math.random() * this.deck.length);
      this.card = this.deck[chosenNumber]; // pick the card in the deck
      this.deck.splice(chosenNumber, 1); // remove the card in the deck
      return this.card;
    },
    pickACard: function() {
      console.log(this.persons);
      this.pick();
      this.persons[this.round].cards.push(this.card);
      this.persons[this.round].status = "En attente";
      if (this.round + 1 === this.persons.length) {
        this.round = 0;
      } else {
        this.round++;
      }
      this.persons[this.round].status = "Joue";
      console.log(this.round);
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
