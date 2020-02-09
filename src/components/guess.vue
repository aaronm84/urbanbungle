<template>
    <v-card class="mx-auto my-6 p-8">
        <v-card-text>
            <h4>{{guess.definition}}</h4>
            <small v-show="isVisible"><i>{{guess.word}}</i></small>
        </v-card-text>
        <v-card-actions>
            <v-btn v-on:click="selection(guess)" :disabled="isDisabled" large color="purple">My Guess</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    props: ['guess', 'isDisabled', 'isVisible'],
    methods: {
        selection() {
            this.$parent.selection(this.guess);
        }
    }
}
</script>


