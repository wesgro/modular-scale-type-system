<template>
<div class="controls">
  <label><div>Heading Ratio {{headingScale}}</div>
    <input type="range" min="1" max="4" step="0.001" v-model="headingScale" />
  </label>
  <label><div>Heading Base size (in rems)</div>
    <input type="number" min="1" max="4" step="0.1" v-model="headingBase" />
  </label>
   <label><div>Sub Heading Ratio {{subHeadingScale}}</div>
    <input type="range" min="1" max="4" step="0.001" v-model="subHeadingScale" />
  </label>
  <label><div>Sub Heading Base size (in rems)</div>
    <input type="number" min="1" max="4" step="0.1" v-model="subHeadingBase" />
  </label>
</div>
<div class="wrapper" :style="getCssVars">
  <template v-for="i in 6" :key="i">
    <div class="holder">
      <div class="headings" :class="`headings--${i}`">The quick brown fox jumps over the lazy dog</div>
      <div class="sub-headings" :class="`sub-headings--${i}`">
        The quick brown fox jumps over the lazy dog
      </div>
    </div>
  </template>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      headingScale: 1.618,
      headingBase: 1.3,
      subHeadingScale: 1.125,
      subHeadingBase: 1.2,
    }
  },
  computed: {
    getCssVars() {
      return {
        '--headings-scale': this.headingScale,
        '--sub-headings-scale': this.subHeadingScale,
        '--size-headings--0': this.headingBase + 'rem',
        '--size-sub-headings--0': this.subHeadingBase + 'rem',
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@use '../style/helpers/helpers.typography' as typography;
@include  typography.generate-heading-styles();
.wrapper{
   @include typography.generate-css-variables();
   margin-left: 16rem;
   overflow-y: auto;
}
.wrapper > * + * {
  margin-top: 2rem;
}

.holder {
  padding: 1.5rem;
}

.controls {
  position: fixed;
  left: 0;
  top: 0;
  border-right: .5rem dashed black;
  border-bottom: .5rem dashed black;
  padding: 1rem;
  background-color: #fff;
  opacity: 0.5;

  &:hover,
  &:focus-within {
    opacity: 1;
  }
  max-width: 15rem;
}
</style>
