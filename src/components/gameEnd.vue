<template>
    <div class="game__end">
      Game over 
      {{statistic.spellCasted}} spell casted
    </div>
</template>

<script>
export default {
  name: 'GameEnd',
  props: {
     statistic: Object
  },
}
</script>

<style>

</style>
