<template>
  <div class="selector-visualisation">
    {{ head }}
    <selector-visualisation
      v-if="tail && tail.length && depth < maxDepth"
      :depth="depth + 1"
      :max-depth="maxDepth"
      :selectorString="tail">
    </selector-visualisation>
  </div>
</template>

<script>
export default {
  name: 'selector-visualisation',
  props: {
    depth: {
      type: Number,
      required: true,
    },
    maxDepth: {
      type: Number,
      required: true,
    },
    selectorString: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
    };
  },
  computed: {
    head() {
      const firstIndex = this.selectorString.indexOf(' ');
      if (firstIndex < 0) {
        return this.selectorString;
      }
      return this.selectorString.slice(0, firstIndex + 1).trim();
    },
    tail() {
      const firstIndex = this.selectorString.indexOf(' ');
      if (firstIndex < 0) {
        return null;
      }
      return this.selectorString.slice(firstIndex + 1, this.selectorString.length).trim();
    },
  },
};
</script>

<style scoped>
  .selector-visualisation {
    background: rgba(66, 185, 131, 0.1);
    border: rgba(66, 185, 131, 0.8) solid 1px;
    padding: 5px;
    margin-top: 5px;
    font-size: 14px;
  }
</style>
