<template>
    <div class="sub-headings" :class="`sub-headings--${level}`"><slot /></div>
</template>

<script>
export default {
  name: 'SubHeading',
  props: {
    level: [String, Number]
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@use '../style/helpers/helpers.typography' as typography;

</style>
