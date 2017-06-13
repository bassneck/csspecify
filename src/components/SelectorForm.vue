<template>
  <div class="hello">
    <h1>CSSpecify</h1>
    <input class="selector-input" type="text" v-model="selectorString"/>
    <ul>
      <li v-for="token in tokens">{{token}}</li>
    </ul>
    <h2>specificity: {{ specificity }}</h2>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data() {
    return {
      selectorString: 'ul#bacon.foo li.bar p #crispy',
      idMatcher: /#[A-z0-9-_]+/g,
      classMatcher: /\.[A-z0-9-_]+/g,
      tagMatcher: /(?:^| )\w+/g,
    };
  },
  methods: {
    extractTokens(regex) {
      const match = this.selectorString.match(regex);
      if (!match) {
        return [];
      }
      return match;
    },
  },
  computed: {
    idTokens() {
      return this.extractTokens(this.idMatcher);
    },
    classTokens() {
      return this.extractTokens(this.classMatcher);
    },
    tagTokens() {
      return this.extractTokens(this.tagMatcher);
    },
    tokens() {
      return this.idTokens.concat(this.classTokens).concat(this.tagTokens);
    },
    specificity() {
      let result = '';
      result += this.idTokens.length.toString();
      result += this.classTokens.length.toString();
      result += this.tagTokens.length.toString();
      return result;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

h1 {
  font-size: 100px;
  margin: 20px 0 60px;
}

.selector-input {
  display: block;
  margin: 0 auto;
  height: 60px;
  width: 600px;
  font-size: 40px;
  font-weight: lighter;
  padding: 10px 20px;
  text-align: center;
}

a {
  color: #42b983;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}
</style>
