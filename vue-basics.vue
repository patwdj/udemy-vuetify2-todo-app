<template>
  <v-container padding>
    <button
      style="position:absolute; right: 10px"
      @click="counter++">{{ counter }}</button>
    <input 
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      v-bind:class="{'error':message.length > 22}"
      ref="messageInput"/>

    <button @click="clearMessage">Clear</button>

    <div> word count: {{ message.length }}</div>

    <h5 
      v-if="message.length"
      class="border-grey">{{message}}</h5>
    <h6 v-else> No message entered </h6>

    <hr>

    <p>Uppercase message: {{ messageUppercase }} </p>
    <p>Lowercase message: {{ message | messageLowercase }}</p>

  </v-container>
</template>

<script>
  export default {
    data() {
      return {
        message: 'test 2',
        counter: 0
      }
    },
    //computed property only fired when message is changed (vs method which are fired everytime)
    computed: {
      messageUppercase() {
        return this.message.toUpperCase()
      },
    },
    methods: {
      clearMessage() {
        this.message = ''
      },
      alertMessage(){
        alert(this.message)
      }
    },
    filters: {
      messageLowercase(value){
        return value.toLowerCase()
      }
    },
    directives: {
      autofocus: {
        inserted(el){
          el.focus()
        }
      }
    },
    beforeCreate(){
      console.log("beforeCreate")
    },
    created(){
      console.log("created")
    },
    beforeMount(){
      console.log("beforeMount")
    },
    mounted(){
      console.log(this.$refs)
    },
    beforeUpdate(){
      console.log("beforeUpdate")
    },
    beforeDestroy(){
      console.log('beforeDestroy')
    },
    destroyed(){
      console.log('destroyed')
    }
  }
</script>

<style>
.border-grey {
  border: 1px solid grey;
}
input, button{
  font-size: 23px;
}
.error {
  background: red;
  color:pink;
}

</style>

<!-- lifecycle hooks: 
beforeCreate() -> created() -> beforeMount() -> mounted()

Vue Component view is updated:
beforeUpdate() -> updated()

Vue Component is destroyed (e.g. moving pages)
beforeDestroy() -> destroyed() -->


<!-- Injecting style
  through class: put the class in <style>: v-bind:class="{className}" 
  through style directly: put in the <v-container> v-bind:style="{StylePutInMethod()}"
 -->
