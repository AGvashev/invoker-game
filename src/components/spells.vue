<template>
    <div class="settings">
        <h2>Spells</h2>
        <div class="spells">
            <div 
            v-for="spell in spells" 
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
  name: 'Settings',
  props: ['settings'],
  data() {
      return {
          spells: {
            ColdSnap: {
              name: 'Cold Snap',
              image: require('@/assets/spells/coldsnap.svg'),
              castBtns: [this.settings.Quas.button, this.settings.Quas.button, this.settings.Quas.button]
            },
            GhostWalk: {
              name: 'Ghost Walk',
              image: require('@/assets/spells/ghostwalk.svg'),
              castBtns: [this.settings.Quas.button, this.settings.Quas.button, this.settings.Wex.button]
            },
            IceWall: {
              name: 'Ice wall',
              image: require('@/assets/spells/icewall.svg'),
              castBtns: [this.settings.Quas.button, this.settings.Quas.button, this.settings.Exort.button]
            },
            EMP: {
              name: 'EMP',
              image: require('@/assets/spells/emp.svg'),
              castBtns: [this.settings.Wex.button, this.settings.Wex.button, this.settings.Wex.button]
            },
            Tornado: {
              name: 'Tornado',
              image: require('@/assets/spells/tornado.svg'),
              castBtns: [this.settings.Wex.button, this.settings.Wex.button, this.settings.Quas.button]
            },
            Alacrity: {
              name: 'Alacrity',
              image: require('@/assets/spells/alacrity.svg'),
              castBtns: [this.settings.Wex.button, this.settings.Wex.button, this.settings.Exort.button]
            },
            SunStrike: {
              name: 'Sun strike',
              image: require('@/assets/spells/sunstrike.svg'),
              castBtns: [this.settings.Exort.button, this.settings.Exort.button, this.settings.Exort.button]
            },
            ForgeSpirit: {
              name: 'Forge spirit',
              image: require('@/assets/spells/forgespirit.svg'),
              castBtns: [this.settings.Exort.button, this.settings.Exort.button, this.settings.Quas.button]
            },
            ChaosMeteor: {
              name: 'Chaos meteor',
              image: require('@/assets/spells/chaosmeteor.svg'),
              castBtns: [this.settings.Exort.button, this.settings.Exort.button, this.settings.Wex.button]
            },
            DefeaningBlast: {
              name: 'Defeaning blast',
              image: require('@/assets/spells/defeaningblast.svg'),
              castBtns: [this.settings.Quas.button, this.settings.Wex.button, this.settings.Exort.button]
            }
          }
      }
  }
}
</script>

<style>
.spells {
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
