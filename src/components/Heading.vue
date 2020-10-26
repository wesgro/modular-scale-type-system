<template>
    <div class="headings" :class="`headings--${level}`"><slot /></div>
</template>

<script>
export default {
  name: 'Heading',
  props: {
    level: [String, Number]
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@use '../style/helpers/helpers.typography' as typography;

</style>
