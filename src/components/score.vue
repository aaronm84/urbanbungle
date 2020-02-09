<template>
    <div class="text-center">
        <h3>Score</h3>
        <h4>{{score}} correct out of {{total}} questions</h4>
    </div>
</template>

<script>
export default {
    props: [
        'score',
        'total'
    ]
}
</script>