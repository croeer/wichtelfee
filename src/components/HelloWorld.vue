<template>
  <div class="hello">
    <h1>Wichtelfee</h1>
    <div align="right">
      <input type="text" v-model='token' placeholder="smptjs token">
    </div>
    <img src="../assets/wichtel.jpg">
    <section>
      Teilnehmer hinzufügen:
      <input type="search" name="search" placeholder="name" @keyup.enter="addWichtel" v-model="newWichtel"/>
       <button class="Search__button" @click="addWichtel">Add</button>
    </section>
    <section>
      <ul>
        <li v-for="w in wichtel" :key="w">
           <div class="view">
          <label @dblclick="editWichtel(w)">{{ w }}</label>
          <button class="destroy" @click="removeWichtel(w)"></button>
        </div>
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
      wichtel: ['test'],
      token: ''
    }
  },
  methods: {
    addWichtel() {
      if(!this.newWichtel.trim()) {return}
      this.wichtel.push(this.newWichtel);
      this.newWichtel = '';
    },
    removeWichtel: function (w) {
      this.wichtel.splice(this.wichtel.indexOf(w), 1)
    },
    composeList() {
      console.log(this.token)
      
      Email.send("phueghy@gmx.de",
      "christian@roeer.info",
      "This is a subject",
      "this is the body",
      {token: this.token});
      
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

li.editing .view {
	display: none;
}

li .destroy {
	display: none;
	/*position: absolute;
	/*
  top: 0;
	right: 10px;
	bottom: 0;
	width: 40px;
	height: 40px;
	margin: auto 0;
  
	font-size: 30px;*/
	color: #cc9a9a;
	/* margin-bottom: 11px; */
	transition: color 0.2s ease-out;
}

li .destroy:hover {
	color: #af5b5e;
}

li .destroy:after {
	content: '×';
}

li:hover .destroy {
	display: inline;
  position: relative;
}

li .edit {
	display: none;
}
</style>
