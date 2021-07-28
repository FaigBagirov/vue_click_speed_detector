<template>
  <div class="theBox" @click="emitClick">
    <p>Click me !</p>
  </div>
</template>

<script>
export default {
  props: {
  },
  data() {
    return {
    }
  },
  methods: {
      emitClick: function(){
        this.$emit('clicked');
      }
  }
}
</script>

<style>
.theBox{
  width: 500px;
  height: 500px;
  margin: 15px auto;
  border: 1px solid green;
  background-color: #ADEFD1FF;
}
.theBox p{
  margin: 46% auto;
  font-size: 3rem !important;
  color: #00203FFF;
}
</style>
