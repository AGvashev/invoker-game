<template>
    <div>
        <div class="cast__panel">
            <div v-for="(cast, i) in castPanel" :key="i" class="cast__circle">
                <img 
                :src="cast == settings.Quas.button ? settings.Quas.image : 
                cast == settings.Wex.button ? settings.Wex.image :
                cast == settings.Exort.button ? settings.Exort.image : ' '" 
                class="cast__circle__image" 
                >
            </div>
        </div>
        <div class="spell__panel">
            <div class="spell quas__panel" @click="quasClick">
                <div class="spell__button">{{ settings.Quas.button }}</div>
                <img src="@/assets/quas.jpg" class="spell__image" alt="Quas">
            </div>
            <div class="spell wex__panel" @click="wexClick">
                <div class="spell__button">{{ settings.Wex.button }}</div>
                <img src="@/assets/wex.jpg" class="spell__image" alt="Wex">
            </div>
            <div class="spell exort__panel" @click="exortClick">
                <div class="spell__button">{{ settings.Exort.button }}</div>
                <img src="@/assets/exort.jpg" class="spell__image" alt="Exort">
            </div>
            <div class="spell first__spell__panel" @click="firstSpellClick">
                <div class="spell__button">{{ settings.FirstSpell.button }}</div>
                <img 
                :src="castPanelSpell[1] != null ? castPanelSpell[1].Image : ' '" 
                class="spell__image"
                >
            </div>
            <div class="spell second__spell__panel" @click="secondSpellClick">
                <div class="spell__button">{{ settings.SecondSpell.button }}</div>
                <img 
                :src="castPanelSpell[0] != null ? castPanelSpell[0].Image : ' '" 
                class="spell__image"
                >
            </div>
            <div class="spell invoke__panel" @click="invokeClick">
                <div class="spell__button">{{ settings.Invoke.button }}</div>
                <img src="@/assets/invoke.jpg" class="spell__image" alt="Invoke">
            </div>
        </div>
    </div>
</template>

<script>

export default {
  name: 'SpellsPanel',
  props: ['settings', 'allSpells'],
  data() {
      return {
          castPanel: [null, null, null],
          castPanelSpell: [null, null]
      }
  },
  methods: {
      quasClick() {
        console.log('Quas click')
        this.castPanel.shift()
        this.castPanel.push(this.settings.Quas.button)
      },
      wexClick() {
        console.log('Wex click')
        this.castPanel.shift()
        this.castPanel.push(this.settings.Wex.button)
      },
      exortClick() {
        console.log('Exort click')
        this.castPanel.shift()
        this.castPanel.push(this.settings.Exort.button)
      },
      firstSpellClick() {
        console.log('First spell click')
      },
      secondSpellClick() {
        console.log('Second spell click')
      },
      invokeClick() {
        console.log('Invoke click')
        if (this.castPanel[0] == null || this.castPanel[1] == null || this.castPanel[2] == null) {
            return
        } else {
            for (let spell in this.allSpells) {
                let castPanelSort = this.castPanel.slice()
                if (this.allSpells[spell].castBtns.sort().join(',') == castPanelSort.sort().join(',')) {
                    this.castPanelSpell.shift()
                    this.castPanelSpell.push({ Name: this.allSpells[spell].name, Image: this.allSpells[spell].image})
                }
            }
        }
      }
  }
}
</script>

<style>
.cast__panel {
    display: flex;
    flex-direction: row;
    justify-content: center;
}

.cast__circle {
    width: 90px;
    height: 90px;

    margin: 0 4px;

    border: 2px solid rgb(201, 201, 201);
    border-radius: 50%;
}

.cast__circle__image {
    width:100%;
    border-radius: 50%;
}

.spell__panel {
    display: flex;
    flex-direction: row;
    background-color: rgb(73, 73, 73);
    padding: 10px 10px 25px;
    border: 2px solid rgb(141, 141, 141);
    border-style: outset;
}

.spell {
    position: relative;
    width: 80px;
    height: 80px;
    margin: 0 5px;
    background: url('../assets/blankspell.png') no-repeat center, rgb(15, 15, 15);
    background-size: contain;
    border: 4px solid rgb(39, 39, 39);
    border-style: outset;
    cursor: pointer;
}

.spell__button {
    position: absolute;
    top: -10px;
    left: -10px;

    font-size: 12px;
    padding: 2px;
    background-color: rgba(90, 90, 90, 0.9);
}

.spell__image {
    /* border: 3px solid green; */
    display: block;
    width: 100%;
}
</style>
