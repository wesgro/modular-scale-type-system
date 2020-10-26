<template>
<div class="controls">
  <label><div>Heading Ratio <code>{{headingScale}}</code></div>
    <input type="range" min="1.5" max="1.9" step="0.001" v-model="headingScale" />
  </label>
  <label><div>Heading Base size (in rems)</div>
    <input type="number" min="1" max="4" step="0.1" v-model="headingBase" />
  </label>
   <label><div>Sub Heading Ratio <code>{{subHeadingScale}}</code></div>
    <input type="range" min="1" max="1.3" step="0.001" v-model="subHeadingScale" />
  </label>
  <label><div>Sub Heading Base size (in rems)</div>
    <input type="number" min="1" max="4" step="0.1" v-model="subHeadingBase" />
  </label>
</div>
<div class="wrapper" :style="getCssVars">
  <template v-for="i in 6" :key="i">
    <div class="holder">
      <div class="holder__level">Size {{i}}</div>
      <Heading :level="7 - i">The quick brown fox jumps over the lazy dog</Heading>
      <SubHeading :level="7 - i">
        The quick brown fox jumps over the lazy dog
      </SubHeading>
    </div>
  </template>
  </div>
</template>

<script>
import Heading from './Heading'
import SubHeading from './SubHeading'
export default {
  name: 'HelloWorld',
  components: {
    Heading,
    SubHeading,
  },
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
   margin-left: 20rem;
  
}

.wrapper > * + * {
  margin-top: 1rem;
}

.holder {
  padding: 1.5rem;
  padding-top: 2.5rem;
  background-color: GhostWhite;
  border: .3rem dashed #5a6974;
  position: relative;
  overflow: hidden;
  
  > * {
    white-space: nowrap;
    transition: 0.15s font-size linear;
    transform: translateZ(0);
    will-change: font-size;
  }

  .holder__level {
    position: absolute;
    top: .5rem;
    left: .5rem;
    line-height: 1;
    font-size: .875rem;
    background-color: #fff;
    z-index: 1;
  }

  *:nth-child(3) {
    margin-top: 1em;
  }
}

.controls {
  @include typography.generate-css-variables();
  position: fixed;
  left: 0;
  top: 0;
  border-right: .5rem dashed black;
  border-bottom: .5rem dashed black;
  padding: 1rem;
  background-color: #fff;
  opacity: 0.5;
  > * + * {
    margin-top: 1rem;
  }
  > *:nth-child(3) {
    margin-top: var(--size-sub-headings--4);
  }
  &:hover,
  &:focus-within {
    opacity: 1;
  }
  max-width: 15rem;
  label {
    display: block;
  }
  input {
    width: 100%;
    display: block;
  }
}
</style>
