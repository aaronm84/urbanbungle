<template>
  <div>
    <Header/>
    <Score :score="score" :total="total"/>
    <Quiz/>
 </div>
</template>

<script>
import Header from './header'
import Score from './score'
import Quiz from './quiz'

export default {
  components : {
    'Header': Header,
    'Score': Score,
    'Quiz': Quiz
  },
  data() {
    return {
      score: 0,
      total: 0
    }
  }
}
</script>

<style>

</style>
