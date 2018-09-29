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
        <li v-for="w in wichtel" :key="w">
           <div class="view">
          <label @dblclick="editWichtel(w)">{{ w }}</label>
          <button class="destroy" @click="removeWichtel(w)"></button>
        </div>
        </li>
      </ul>
    </section>
    <section>
      <button @click="testlist">Würfeln</button>
    </section>
    <section>
      <ul v-if="showResults">
        <li v-for="r in resultList" :key="r.name">
              {{ r.name }} -> {{ r.partner }} <a :href="r.text">mail</a>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
function shuffle(a) {
    for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
    }
    return a;
}

function checkLists(a,b) {
  if (a.length < 2) {
    return true;
  }
  for (var i=0; i < a.length; i++) {
    if (a[i]==b[i]){
      return false;
    }
  }
  return true;
}

export default {
  name: 'HelloWorld',
  data () {
    return {
      newWichtel: '',
      wichtel: [1,2,3,4,5,6,7,8,9],
      showResults: false,
      resultList: []
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
    testlist() {
      this.resultList.length = 0;
      var l = this.wichtel.slice(0);
      shuffle(l);
      while (!checkLists(this.wichtel, l)) {
        shuffle(l);
      }
      console.log(l);
      for (var i=0; i < this.wichtel.length; i++) {
        var linktext = "mailto:" + this.wichtel[i] 
        + "?subject=Wichtelfee: Dein Wichtelpartner&"
        + "body=Hallo " + this.wichtel[i] + ",%0d%0a%0d%0a"
        + "Dein Wichtelpartner ist:%0d%0a%0d%0a"
        + l[i] + "%0d%0a%0d%0a"
        + "Viele Grüße,%0d%0a%0d%0a"
        + "Deine Wichtelfee";

        var o = {
          name:this.wichtel[i],
          partner:l[i],
          text:linktext
        };
        this.resultList.push(o);
      }
      this.showResults = true;
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
