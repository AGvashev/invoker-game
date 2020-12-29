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
                <div class="spell__button">{{ !legacyKey ? settings.FirstSpell.button : castPanelSpell[1].button }}</div>
                <img 
                :src="castPanelSpell[1].name != null ? castPanelSpell[1].Image : ' '" 
                class="spell__image"
                >
            </div>
            <div class="spell second__spell__panel" @click="secondSpellClick">
                <div class="spell__button">{{ !legacyKey ? settings.SecondSpell.button : castPanelSpell[0].button}}</div>
                <img 
                :src="castPanelSpell[0].name != null ? castPanelSpell[0].Image : ' '" 
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
  props: {
      settings: Object,
      allSpells: Object,
      statistic: Object,
      gameSpells: Array,
      legacyKey: Boolean,
      castedSpells: Number
  },
  data() {
      return {
          castPanel: [null, null, null],
          castPanelSpell: [{name: null}, {name: null}],
          timerCount: 50,
      }
  },
  methods: {
      quasClick() {
        this.castPanel.shift()
        this.castPanel.push(this.settings.Quas.button)
      },
      wexClick() {
        this.castPanel.shift()
        this.castPanel.push(this.settings.Wex.button)
      },
      exortClick() {
        this.castPanel.shift()
        this.castPanel.push(this.settings.Exort.button)
      },
      firstSpellClick() {
        if (this.castPanelSpell[1].name == null) return
        this.statistic.spellCasted++
        // let spellCompleteIndex = null
        this.gameSpells.forEach((el, ) => {
            if (this.castPanelSpell[1].name == el.name) {
                this.statistic.trueSpells++
                el.casted = true
                this.gameSpells.splice()
            }
        })
      },
      secondSpellClick() {
        if (this.castPanelSpell[1].name == null) return
        this.statistic.spellCasted++
        // let spellCompleteIndex = null
        this.gameSpells.forEach((el, ) => {
            if (this.castPanelSpell[0].name == el.name) {
                this.statistic.trueSpells++
                el.casted = true
                this.gameSpells.splice()
            }
        })
      },
      invokeClick() {
        if (this.castPanel[0] == null || this.castPanel[1] == null || this.castPanel[2] == null) {
            return
        } else {
            for (let spell in this.allSpells) {
                let castPanelSort = this.castPanel.slice()
                if (this.allSpells[spell].castBtns.sort().join(',') == castPanelSort.sort().join(',')) {
                    if (this.castPanelSpell[1].name == this.allSpells[spell].name) return
                    this.castPanelSpell.shift()
                    if (this.legacyKey) {
                        this.castPanelSpell.push({ name: this.allSpells[spell].name, Image: this.allSpells[spell].image, button: this.settings[spell].button})
                    } else {
                        this.castPanelSpell.push({ name: this.allSpells[spell].name, Image: this.allSpells[spell].image})
                    }
                }
            }
        }
      },
      keyPressed(key) {
        const keyPressedNow = key.key
        this.statistic.keyPressed++
        if (keyPressedNow.toUpperCase() == this.settings.Quas.button) {
            this.quasClick()
        }else if (keyPressedNow.toUpperCase() == this.settings.Wex.button) {
            this.wexClick()
        }else if (keyPressedNow.toUpperCase() == this.settings.Exort.button) {
            this.exortClick()
        }else if (keyPressedNow.toUpperCase() == this.settings.Invoke.button) {
            this.invokeClick()
        }
        if (!this.legacyKey) {
            if (keyPressedNow.toUpperCase() == this.settings.FirstSpell.button) {
                this.firstSpellClick()
            } else if (keyPressedNow.toUpperCase() == this.settings.SecondSpell.button) {
                this.secondSpellClick()
            }
        } else {
            if (keyPressedNow.toUpperCase() == this.castPanelSpell[0].button) {
                this.secondSpellClick()
            } else if (keyPressedNow.toUpperCase() == this.castPanelSpell[1].button) {
                this.firstSpellClick()  
            }
        }
      }
  },
  mounted() {
    window.addEventListener('keydown', this.keyPressed)
  },
  beforeDestroy() {
    window.removeEventListener('keydown', this.keyPressed)
  },
  beforeUpdate() {
    if (this.legacyKey) {
        for (let spell in this.settings) {
            if (this.settings[spell].name == this.castPanelSpell[0].name) this.castPanelSpell[0].button = this.settings[spell].button
            if (this.settings[spell].name == this.castPanelSpell[1].name) this.castPanelSpell[1].button = this.settings[spell].button
        }  
    }
  }
}
</script>

<style>
.timer__line {
    height: 20px;
    border-radius: 20px;
    background-color: red;
}

.cast__panel {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin-bottom: 50px;
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
