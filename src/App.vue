<template>
  <div id="app">
    <div v-if="preloader" class="preloader">
      <img src="@/assets/preloader.png" alt="Preloader" style="width:200px">
    </div>
    <div class="container">
      <div class="app__content">
        <div class="leftside">
            <Settings
            :settings = keys
            />
            <label style="display:block;">
            <input type="checkbox" name="legacy" class="legacy__key__setting" @change="legacyKey" v-model="legacy">
            Use legacy key
            </label>
            <div v-if="!legacy" class="buttons">
              <button @click="settingConfigurate"> Configurate </button>
              <button @click="settingReset"> Reset </button>
            </div>
        </div>
        <div class="middleside">
         <SpellsPanel 
         :settings = keys
         :allSpells = spells
         :legacyKey = legacy
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
import SpellsPanel from './components/spellsPanel.vue'

export default {
  name: 'App',
  components: {
    Settings,
    Spells,
    SpellsPanel
  },
  data() {
      return {
          legacy: false,
          preloader: true,
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
          castBtns: [this.keys.Quas.button, this.keys.Quas.button, this.keys.Quas.button]
        },
        GhostWalk: {
          name: 'Ghost Walk',
          image: require('@/assets/spells/ghostwalk.svg'),
          castBtns: [this.keys.Quas.button, this.keys.Quas.button, this.keys.Wex.button]
        },
        IceWall: {
          name: 'Ice Wall',
          image: require('@/assets/spells/icewall.svg'),
          castBtns: [this.keys.Quas.button, this.keys.Quas.button, this.keys.Exort.button]
        },
        EMP: {
          name: 'EMP',
          image: require('@/assets/spells/emp.svg'),
          castBtns: [this.keys.Wex.button, this.keys.Wex.button, this.keys.Wex.button]
        },
        Tornado: {
          name: 'Tornado',
          image: require('@/assets/spells/tornado.svg'),
          castBtns: [this.keys.Wex.button, this.keys.Wex.button, this.keys.Quas.button]
        },
        Alacrity: {
          name: 'Alacrity',
          image: require('@/assets/spells/alacrity.svg'),
          castBtns: [this.keys.Wex.button, this.keys.Wex.button, this.keys.Exort.button]
        },
        SunStrike: {
          name: 'Sun Strike',
          image: require('@/assets/spells/sunstrike.svg'),
          castBtns: [this.keys.Exort.button, this.keys.Exort.button, this.keys.Exort.button]
        },
        ForgeSpirit: {
          name: 'Forge Spirit',
          image: require('@/assets/spells/forgespirit.svg'),
          castBtns: [this.keys.Exort.button, this.keys.Exort.button, this.keys.Quas.button]
        },
        ChaosMeteor: {
          name: 'Chaos Meteor',
          image: require('@/assets/spells/chaosmeteor.svg'),
          castBtns: [this.keys.Exort.button, this.keys.Exort.button, this.keys.Wex.button]
        },
        DeafeningBlast: {
          name: 'Deafening Blast',
          image: require('@/assets/spells/defeaningblast.svg'),
          castBtns: [this.keys.Quas.button, this.keys.Wex.button, this.keys.Exort.button]
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
</style>
