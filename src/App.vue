<template>
  <div id="app">
    <div v-if="preloader" class="preloader">
      <img src="@/assets/preloader.png" alt="Preloader" style="width:200px">
    </div>
    <div class="container">
      <div class="app__content">
        <div class="leftside">
          <div class="settings__block">
            <Settings
            :settings = keys
            />
            <label style="display:block;">
            <input type="checkbox" name="legacy" class="legacy__key__setting" @change="legacyKey" v-model="legacy">
            Use legacy key
            </label>
            <div v-if="!legacy" class="buttons">
              <!-- <button @click="settingConfigurate"> Configurate </button> 
              <button @click="settingReset"> Reset </button> -->
            </div>
          </div>
           <div class="statistic__block">
              <div
              v-for="( stat, name, index ) in statistic"
              :key="index"
              >
                {{ 
                  name == 'keyPressed' ? 'Key pressed' :
                  name == 'spellCasted' ? 'Spell casted' :
                  name == 'trueSpells' ? 'True spells casted' : ''
                }}:
                {{ stat }}
              </div>
           </div>
        </div>
        <div class="middleside">
          <h2 v-if="gameMode == 'none'" class="game__mode__title">Select the game mode</h2>
          <h2 v-if="gameMode != 'none'" class="game__mode__title backtomenu__title">Back to menu</h2>
          <button v-if="gameMode != 'none'" class="main__menu__btn" @click="gameMode = 'none'">Main menu</button>
          <div v-if="gameMode == 'none'">
            <button class="game__mode__btn" @click="gameMode = 'Survival'">Survival</button>
            <button class="game__mode__btn" @click="gameMode = 'Classic'">Classic</button>
            <button class="game__mode__btn" @click="gameMode = '3xCombo'">3x Combo</button>
            <button class="game__mode__btn" @click="gameMode = 'Endless'">Endless</button>
          </div>
          <Game
          v-if="gameMode != 'none'"
          :gameMode = gameMode
          :settings = keys
          :allSpells = spells
          :legacyKey = legacy
          :statistic = statistic
           />
        </div>
        <div class="rightside">
          <Spells
          :settings = keys
          :allSpells = spells
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Settings from './components/settings.vue'
import Spells from './components/spells.vue'
import Game from './components/game.vue'

export default {
  name: 'App',
  components: {
    Settings,
    Spells,
    Game,
  },
  data() {
      return {
          legacy: false,
          preloader: true,
          gameMode: 'none',
          keys: {
            Quas: {
                name: 'Quas',
                image: require('@/assets/quas.jpg'),
                button: 'Q'
            },
            Wex: {
                name: 'Wex',
                image: require('@/assets/wex.jpg'),
                button: 'W'
            },
            Exort: {
                name: 'Exort',
                image: require('@/assets/exort.jpg'),
                button: 'E'
            },
            Invoke: {
                name: 'Invoke',
                image: require('@/assets/invoke.jpg'),
                button: 'R'
            },
            FirstSpell: {
                name: 'First spell',
                button: 'D'
            }, 
            SecondSpell: {
                name: 'Second spell',
                button: 'F'
            }
          },
          spells: {
          },
          statistic: {
              keyPressed: 0,
              spellCasted: 0,
              trueSpells: 0
          }
      }
  },
  methods: {
    settingReset() {
      this.keys = {
            Quas: {
              name: 'Quas',
              image: require('@/assets/quas.jpg'),
              button: 'Q'
            },
            Wex: {
                name: 'Wex',
                image: require('@/assets/wex.jpg'),
                button: 'W'
            },
            Exort: {
                name: 'Exort',
                image: require('@/assets/exort.jpg'),
                button: 'E'
            },
            Invoke: {
                name: 'Invoke',
                image: require('@/assets/invoke.jpg'),
                button: 'R'
            },
            FirstSpell: {
                name: 'First spell',
                button: 'D'
            }, 
            SecondSpell: {
                name: 'Second spell',
                button: 'F'
            }
          }
    },
    settingConfigurate() {

    },
    legacyKey() {
      if (this.legacy) {
        this.keys = {
            Quas: {
              name: 'Quas',
              image: require('@/assets/quas.jpg'),
              button: 'Q'
            },
            Wex: {
              name: 'Wex',
              image: require('@/assets/wex.jpg'),
              button: 'W'
            },
            Exort: {
              name: 'Exort',
              image: require('@/assets/exort.jpg'),
              button: 'E'
            },
            Invoke: {
              name: 'Invoke',
              image: require('@/assets/invoke.jpg'),
              button: 'R'
            },
            ColdSnap: {
                name: 'Cold Snap',
                button: 'Y'
            },
            GhostWalk: {
                name: 'Ghost Walk',
                button: 'V'
            },
            IceWall: {
                name: 'Ice Wall',
                button: 'G'
            },
            EMP: {
                name: 'EMP',
                button: 'C'
            },
            Tornado: {
                name: 'Tornado',
                button: 'X'
            },
            Alacrity: {
                name: 'Alacrity',
                button: 'Z'
            },
            SunStrike: {
                name: 'Sun Strike',
                button: 'T'
            },
            ForgeSpirit: {
                name: 'Forge Spirit',
                button: 'F'
            },
            ChaosMeteor: {
                name: 'Chaos Meteor',
                button: 'D'
            },
            DeafeningBlast: {
                name: 'Deafening Blast',
                button: 'B'
            },
        }
      } else {
        this.settingReset()
      }
    },
    spellCastBtnUpdate() {
      this.spells = {
        ColdSnap: {
          name: 'Cold Snap',
          image: require('@/assets/spells/coldsnap.svg'),
          castBtns: [this.keys.Quas.button, this.keys.Quas.button, this.keys.Quas.button],
          casted: false
        },
        GhostWalk: {
          name: 'Ghost Walk',
          image: require('@/assets/spells/ghostwalk.svg'),
          castBtns: [this.keys.Quas.button, this.keys.Quas.button, this.keys.Wex.button],
          casted: false
        },
        IceWall: {
          name: 'Ice Wall',
          image: require('@/assets/spells/icewall.svg'),
          castBtns: [this.keys.Quas.button, this.keys.Quas.button, this.keys.Exort.button],
          casted: false
        },
        EMP: {
          name: 'EMP',
          image: require('@/assets/spells/emp.svg'),
          castBtns: [this.keys.Wex.button, this.keys.Wex.button, this.keys.Wex.button],
          casted: false
        },
        Tornado: {
          name: 'Tornado',
          image: require('@/assets/spells/tornado.svg'),
          castBtns: [this.keys.Wex.button, this.keys.Wex.button, this.keys.Quas.button],
          casted: false
        },
        Alacrity: {
          name: 'Alacrity',
          image: require('@/assets/spells/alacrity.svg'),
          castBtns: [this.keys.Wex.button, this.keys.Wex.button, this.keys.Exort.button],
          casted: false
        },
        SunStrike: {
          name: 'Sun Strike',
          image: require('@/assets/spells/sunstrike.svg'),
          castBtns: [this.keys.Exort.button, this.keys.Exort.button, this.keys.Exort.button],
          casted: false
        },
        ForgeSpirit: {
          name: 'Forge Spirit',
          image: require('@/assets/spells/forgespirit.svg'),
          castBtns: [this.keys.Exort.button, this.keys.Exort.button, this.keys.Quas.button],
          casted: false
        },
        ChaosMeteor: {
          name: 'Chaos Meteor',
          image: require('@/assets/spells/chaosmeteor.svg'),
          castBtns: [this.keys.Exort.button, this.keys.Exort.button, this.keys.Wex.button],
          casted: false
        },
        DeafeningBlast: {
          name: 'Deafening Blast',
          image: require('@/assets/spells/defeaningblast.svg'),
          castBtns: [this.keys.Quas.button, this.keys.Wex.button, this.keys.Exort.button],
          casted: false
        }
      }
    }
  },
  mounted() {
    setTimeout(() => {
      this.preloader = false
      this.spellCastBtnUpdate()
    }, 2000);
  }
}
</script>

<style>
/* Preloader animation */
@keyframes preloaderRotate {
  100% {
    transform: rotate(360deg);
  }
}

* {
  padding: 0;
  margin: 0;
}

#app {
  width: 100%;
  height: 100vh;
  background: url('assets/invoker-background.jpg');
  color: #FFF;
}

.preloader {
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background-color:rgb(22,20,23);
  z-index: 999999;
}

.preloader img {
  animation: preloaderRotate 1.5s linear infinite;
}

.app__content {
  display: flex;
  flex-direction: row;
  justify-content: space-around;

  border: 3px solid rgb(255, 255, 255);
  border-radius: 20px;
  padding: 20px;
  background-color: rgba(128, 128, 128, 0.95);
}

.container {
  width: 1400px;
  max-width: 98%;
  margin: 0 auto;
}

.settings__block {
  margin: 10px 0;
  padding: 10px;
  border: 1px solid rgb(212, 212, 212);
  border-radius: 10px;
}

.statistic__block {
  margin: 10px 0;
  padding: 10px;
  border: 1px solid rgb(212, 212, 212);
  border-radius: 10px;
}

.game__mode__title {
  text-transform: uppercase;
}

.rightside {
  margin: 10px 0;
  padding: 10px;
  border: 1px solid rgb(212, 212, 212);
  border-radius: 10px;
}

.game__mode__btn {
  padding: 5px;
  margin: 5px;
}

.main__menu__btn {
  display: inline-block;
  padding: 5px;
  margin: 5px;
}

.backtomenu__title {
  display: inline-block;
}
</style>
