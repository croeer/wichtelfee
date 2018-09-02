<template>
  <div class="hello">
    <h1>Wichtelfee</h1>
    <img src="../assets/wichtel.jpg">
    <section>
      Teilnehmer hinzufügen:
      <input type="search" name="search" placeholder="name" @keyup.enter="addWichtel" v-model="newWichtel"/>
       <button class="Search__button" @click="addWichtel">Add</button>
    </section>
    <section>
      <ul>
        <li v-for="w in wichtel" :key="w">{{ w }}
        </li>
      </ul>
    </section>
    <section>
      <button @click="composeList">Würfeln</button>
    </section>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      newWichtel: '',
      wichtel: ['test']
    }
  },
  methods: {
    addWichtel() {
      if(!this.newWichtel.trim()) {return}
      this.wichtel.push(this.newWichtel);
      this.newWichtel = '';
    },
    composeList() {
      this.wichtel = _.shuffle(this.wichtel)
      ;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
