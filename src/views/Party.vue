<template>
  <div class="home">
    <h1>Your Party:</h1>
    <div v-if="this.$root.$data.party.length===0">
      <p>Your party is empty</p>
    </div>
    <div v-else>
    <p>Total Cost: {{$root.$data.totalcost}} gold</p>
      <section class="image-gallery">
        <div class="image" v-for="adventurer in adventurers" :key="adventurer.id">
          <h2>{{adventurer.name}} <em>({{adventurer.race}})</em></h2>
          <div class="stats item">
            <p>Strength: {{adventurer.strength}}</p>
            <p>Agility: {{adventurer.agility}}</p>
            <p>Durability: {{adventurer.durability}}</p>
            <p>Intelligence: {{adventurer.intelligence}}</p>
          </div>
          <p></p>
          <p>{{adventurer.description}}</p>
          <br>
          <p>Cost: {{adventurer.cost}} gold</p>
          <button v-on:click="$root.$data.party.splice($root.$data.party.indexOf(adventurer),1); $root.$data.totalcost -= adventurer.cost" class="auto">Remove from Party</button>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'Home',
  data() {
    return {
     adventurers: [],
    }
  },
  created() {
    this.getAdventurers();
  },
  methods: {
    getAdventurers() {
      try {
        //let response = this.$root.$data
        this.adventurers = this.$root.$data.adventurers.filter(adventurer => this.$root.$data.party.includes(adventurer.id));
        console.log(this.adventurers);
        return true;
      } catch (error) {
        console.log(error);
      }
    },
  }
}
</script>
