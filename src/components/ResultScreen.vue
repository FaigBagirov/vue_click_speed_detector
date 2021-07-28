<template>
    <div>
        <p>Your timing is: {{theClickSpeed}} ms</p>
        <p>Your rank is:  {{ranks[theRankLevel]}}</p>
    </div>
</template>

<script>
export default{
    props: ['theClickSpeed','theRankLevel'],
    data() {
        return {
            ranks: ["Snail", "Turtle", "Crazy Crab", "Rabbit", "Racing Horse", "Cheetah", "You Are a Machine", "Lightning"],
        }
    }
}
</script>

<style>

</style>
