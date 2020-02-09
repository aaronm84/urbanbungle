<template>
    <div class="d-flex flex-column">
        <v-btn @click="getData" class="align-self-center my-5" large v-bind:class="{ pulseBtn: isActive}">Next Word</v-btn>
        <Word :word="word" class="align-self-center"/>
        <div class="px-10">
            <p>Pick the correct definition</p>
            <Guess v-for="guess in randomGuesses" v-bind:key="guess.id" :guess="guess" :isDisabled="isDisabled" :isVisible="isVisible"/>
        </div>
    </div>
    
</template>

<script>
import axios from 'axios'
import Word from './word'
import Guess from './guess'

export default {
    components: {
        'Word': Word,
        'Guess': Guess
    },
    data() {
        return {
            word: [],
            guesses: [],
            isDisabled: false,
            isVisible: false,
            isActive: false
        }
    },
    methods: {
        getData () {
            this.isDisabled = false,
            this.isVisible = false,
            this.isActive = false,
            axios.get('https://api.urbandictionary.com/v0/random')
            .then(response => {
            this.word = response.data.list[0].word
            this.guesses = [
                {
                id: 0,
                word: response.data.list[0].word,
                definition: response.data.list[0].definition,
                correct: true
                },
                {
                id: 1,
                word: response.data.list[1].word,
                definition: response.data.list[1].definition,
                correct: false
                },
                {
                id: 2,
                word: response.data.list[2].word,
                definition: response.data.list[2].definition,
                correct: false
                }
            ]

            })
        },
        randomize: function(rand) {
            return rand.sort(function(){return 0.5 - Math.random()})
        },
        selection: function(guess) {
            if (guess.correct == true ) {
                alert("Correct!")
                this.isDisabled = true
                this.isVisible = true
                this.isActive = true
                this.$parent.score += 1
                this.$parent.total += 1
                
            } else {
                alert("Incorrect!")
                this.isDisabled = true
                this.isVisible = true
                this.isActive = true
                this.$parent.total += 1
            }
        }
    },
    computed: {
        randomGuesses() {
            return this.randomize(this.guesses)
        }
    },
    created() {
        this.getData()
  }

}
</script>

<style scoped>
@keyframes shadow-pulse
{
  0% {
    box-shadow: 0 0 0 0px rgba(0, 0, 0, 0.2);
  }
  100% {
    box-shadow: 0 0 0 35px rgba(0, 0, 0, 0);
  }
}

@keyframes shadow-pulse-big
{
  0% {
    box-shadow: 0 0 0 0px rgba(0, 0, 0, 0.1);
  }
  100% {
    box-shadow: 0 0 0 70px rgba(0, 0, 0, 0);
  }
}

.pulseBtn
{

  animation: shadow-pulse 1s infinite;
}
</style>