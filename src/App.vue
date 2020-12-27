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
         
        </div>
        <div class="rightside">
          <Spells
          :settings = keys
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Settings from './components/settings.vue'
import Spells from './components/spells.vue'

export default {
  name: 'App',
  components: {
    Settings,
    Spells
  },
  data() {
      return {
          legacy: false,
          preloader: true,
          keys: {
            Quas: {
                name: 'Quas',
                button: 'Q'
            },
            Wex: {
                name: 'Wex',
                button: 'W'
            },
            Exort: {
                name: 'Exort',
                button: 'E'
            },
            Invoke: {
                name: 'Invoke',
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
      }
  },
  methods: {
    settingReset() {
      this.keys = {
            Quas: {
                name: 'Quas',
                button: 'Q'
            },
            Wex: {
                name: 'Wex',
                button: 'W'
            },
            Exort: {
                name: 'Exort',
                button: 'E'
            },
            Invoke: {
                name: 'Invoke',
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
                button: 'Q'
            },
            Wex: {
                name: 'Wex',
                button: 'W'
            },
            Exort: {
                name: 'Exort',
                button: 'E'
            },
            Invoke: {
                name: 'Invoke',
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
                name: 'Deafening Blas',
                button: 'B'
            },
        }
      } else {
        this.settingReset()
      }
    }
  },
  mounted() {
    setTimeout(() => {
      this.preloader = false
    }, 5000);
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
