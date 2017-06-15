<template>
  <div class="hello">
    <h1>CSSpecify</h1>
    <input class="selector-input" type="text" v-model="selectorString"/>
    <div class="specificity-measure">
      <div class="specificity-measure__item">
        <div class="specificity-measure__item__value">
          {{ idTokens.length }}
        </div>
        <div class="specificity-measure__item__label">
          #id
        </div>
      </div>
      <div class="specificity-measure__item">
        <div class="specificity-measure__item__value">
          {{ classTokens.length }}
        </div>
        <div class="specificity-measure__item__label">
          .class
        </div>
      </div>
      <div class="specificity-measure__item">
        <div class="specificity-measure__item__value">
          {{ tagTokens.length }}
        </div>
        <div class="specificity-measure__item__label">
          tag
        </div>
      </div>
    </div>
    <ul class="debug-bar">
      <li v-for="token in tokens">{{token}}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data() {
    return {
      selectorString: 'ul#bacon.foo li.bar p #crispy',
      idMatcher: /#[A-z0-9-_]+/g,
      classMatcher: /(\.[A-z0-9-_]+)/g,
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
  box-sizing: border-box;
  display: block;
  margin: 0 auto 10px;
  height: 60px;
  width: 600px;
  font-size: 40px;
  font-weight: lighter;
  text-align: center;
}

.specificity-measure {
  width: 600px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
}

.specificity-measure__item {
  border: rgb(238, 238, 238) solid 1px;
  flex-grow: 1;
  padding: 10px;
  margin-left: 10px;
}

.specificity-measure__item:first-child {
  margin-left: 0;
}

.specificity-measure__item__value {
  font-size: 80px;
  line-height: 1.1em;
}

.specificity-measure__item__label {

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
