<template>
    <div class="game">
        <div
        v-if="!gameOver"
        >
            <div
            v-if="gameStarted"
            class="game__spells__panel"
            >
                <div 
                class="game__spells__block"
                :class="{ casted : gameSpell.casted }"
                v-for="(gameSpell, i) in gameSpells"
                :key = i
                >
                    <img class="spells__block__img" :src='gameSpell.image' alt="Spell image">
                    <span class="spells__block__text">{{gameSpell.name}}</span> 
                </div>
            </div>
            <div 
            class="timer__line"
            v-if="gameStarted && gameMode != 'Endless' && gameMode != 'Classic'"
            :style="{width: timerLine + '%'}">
            </div>
            
            <SpellsPanel 
            :settings = settings
            :allSpells = allSpells
            :legacyKey = legacyKey
            :gameSpells = gameSpells
            :statistic = statistic
            />
        </div>
        <GameEnd 
        v-if="gameOver"
        :statistic = statistic
        />
        <button class="main__btns" v-if="gameReset" @click="gameCancel">Game reset</button>
        <button class="main__btns"  v-if="!gameStarted" @click="gameStart">Game start (Press ENTER)</button> 
    </div>
</template>

<script>
import SpellsPanel from './spellsPanel.vue'
import GameEnd from './gameEnd.vue'

export default {
    name: 'Game',
    components: {
        SpellsPanel,
        GameEnd
    }, 
    props: {
        settings: Object,
        allSpells: Object,
        legacyKey: Boolean,
        gameMode: String,
        statistic: Object
    },
    data() {
        return {
            gameSpells: [],
            gameStarted: false,
            gameReset: false,
            gameOver: false,
            timer: null,
            timerLineTransitionOff: false,
            timerLine: 100,
            timerCount: 0,
            castSpells: 0,
            spellCount: 0,
        }
    },
    methods: {
        getRandomInt(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        },
        randomSpell() {
            for (const spell in this.allSpells) {
                if (this.allSpells[spell].casted) {
                    this.allSpells[spell].casted = false
                }
            }
            if (this.gameMode == 'Classic' || this.gameMode == 'Endless') {
                this.spellCount = this.getRandomInt(1, 1)
            } else if (this.gameMode == '3xCombo') {
                this.spellCount = this.getRandomInt(3, 3)
            } else if (this.gameMode == 'Survival') {
                this.spellCount = this.getRandomInt(1, 3)
            }     
            this.gameSpells = []
            while (this.gameSpells.length < this.spellCount ) {
                let randNum = this.getRandomInt(0, 9)
                let randSpellKey = Object.keys(this.allSpells)[randNum]
                let randSpell = this.allSpells[randSpellKey]
                if (this.gameSpells.length > 0) {
                    let spellInArr = false
                    this.gameSpells.forEach( el => {
                        if (el == randSpell) {
                            spellInArr = true
                        } 
                    })
                    if (!spellInArr) this.gameSpells.push(randSpell)
                } else {
                    this.gameSpells.push(randSpell)
                }
            }    
        },
        startTimer() {
            const timerCount = 100/this.timerCount
            this.timer = setInterval(() => {
                let newTimerLine = this.timerLine -= timerCount
                if ( newTimerLine < 0) {
                    this.timerLine = 0
                } else {
                    this.timerLine = newTimerLine
                }

                if (this.gameMode == '3xCombo' || this.gameMode == 'Survival') {
                    if (this.timerCount > 0) {
                    this.timerCount-- 
                    }  else {
                        this.stopTimer()
                        this.gameEnd()
                    }
                } else if (this.gameMode == 'Classic'){
                    if (this.timerCount < 30) {
                    this.timerCount++
                    }  else {
                        this.stopTimer()
                        this.gameEnd()
                    }
                }

                
            }, 1000)
        },
        stopTimer() {
            this.timerLine = 100
            clearTimeout(this.timer)
        },
        gameStart() {  
            this.gameStarted = true
            this.gameReset = true
            this.randomSpell()
            if (this.gameMode == '3xCombo') {
                this.timerCount = 30
            } else if (this.gameMode == 'Survival') {
                this.timerCount = this.gameSpells.length * 3
            }  else {
                this.timerCount = 0
            }
            this.startTimer()
        },
        gameEnd() {
            this.gameReset = false
            this.gameOver = true
        },
        gameCancel() {
            this.stopTimer()
            this.timerCount = 0
            this.gameSpells = []
            this.gameStarted = false
            this.gameReset = false
            this.castSpells = 0
            this.statistic.keyPressed = 0 
            this.statistic.spellCasted = 0 
            this.statistic.trueSpells = 0 
        }
    },
    watch: {
        gameSpells: function (arr) {
            let castedSpellCount = null;
            arr.forEach(el => {
                if (el.casted) {
                    castedSpellCount++
                } 
            });
            if (castedSpellCount == this.spellCount && this.gameStarted == true && this.gameMode == 'Classic') {
                // Создать и добавить gameEnd
                this.randomSpell()
            } else if (castedSpellCount == this.spellCount && this.gameStarted == true && this.gameMode == "Survival") {
                this.timerCount = arr.length * (3 - (Math.floor(this.statistic.trueSpells * 0.01)))
                this.timerLine = 100
                this.randomSpell()
                // Добавить обновление таймера и полоски 
            } else if (castedSpellCount == this.spellCount && this.gameStarted == true && this.gameMode == "3xCombo") {
                // Добавить gameEnd 
                this.randomSpell()
            } else if (castedSpellCount == this.spellCount && this.gameStarted == true && this.gameMode == "Endless") {
                // Добавить gameEnd 
                this.randomSpell()
            }
        }
    }
}
</script>

<style>
.timer__line {
    background-color: rgba(15, 122, 38, 0.904);
    border-radius: 20px;
    width: 100%;
    height: 20px;
    margin: 20px 0;
    transition: 1s linear;
}

.casted {
    border: 1px solid rgb(9, 255, 0);
    opacity: .5;
}

.main__btns {
    margin: 5px;
    padding: 5px;
}

.game__spells__panel {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    margin: 50px;
}

.game__spells__block {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    margin: 5px 10px;
    padding: 5px;
}

.spells__block__img {
    width: 80px;
}

.spells__block__text {
    margin: 0 5px;
    font-size: 20px;
    text-transform: uppercase;
}
</style>
