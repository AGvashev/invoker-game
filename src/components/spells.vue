<template>
    <div class="spells">
        <h2>Spells</h2>
        <div class="spells__content">
            <div 
            v-for="spell in allSpells" 
            :key="spell.name"
            >
                <img :src="spell.image" style="width:20px;">
                {{ spell.name }} - 
                <span 
                v-for="(castBtn, i) in spell.castBtns" 
                :key="i"
                :class="castBtn == settings.Quas.button ? 'blue' : 
                castBtn == settings.Exort.button ? 'yellow' : 
                castBtn == settings.Wex.button ? 'purple' : '' "
                >
                    {{ castBtn }}
                </span>
            </div>
        </div>
    </div>
</template>

<script>

export default {
  name: 'Spells',
    props: {
      settings: Object,
      allSpells: Object,
  },
  data() {
      return {
         
      }
  }
}
</script>

<style>
.spells__content {
    display: flex;
    flex-direction: column;
    align-items: left;
}
.blue {
    color:#72C3FC;
}
.purple {
    color:#CE72FC;
}
.yellow {
    color:#FCCA72;
}
</style>
