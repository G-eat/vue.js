<template lang="html">
  <div class="">
    <p class="blue-text text-darken-2">{{ msg }}</p>
    <button type="button" name="button" @click='change_button' v-bind:disabled='button_disabled'>Go</button>
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    msg: String
  },
  data (){
    return {
      button_disabled : false
    }
  },
  methods: {
    change_button() {
      this.button_disabled = !this.button_disabled;
    }
  }
}
</script>

<style lang="css" scoped>
  @import url('https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css');
</style>
