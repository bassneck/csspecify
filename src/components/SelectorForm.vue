<template>
  <div class="selector-form">
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
    <selector-visualisation
      :depth="0"
      :max-depth="10"
      :selectorString="selectorString">
    </selector-visualisation>
  </div>
</template>

<script>
import SelectorVisualisation from './SelectorVisualisation';

export default {
  components: { SelectorVisualisation },
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
.selector-form {
  width: 600px;
  margin: 0 auto;
}

.selector-input {
  box-sizing: border-box;
  display: block;
  margin-bottom: 10px;
  height: 60px;
  width: 100%;
  font-size: 40px;
  font-weight: lighter;
  text-align: center;
}

.specificity-measure {
  display: flex;
  justify-content: space-between;
}

.specificity-measure__item {
  border: rgb(238, 238, 238) solid 1px;
  flex-grow: 1;
  padding: 10px;
  margin-left: 10px;
  position: relative;
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
