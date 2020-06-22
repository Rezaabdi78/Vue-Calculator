<template>
<div class=" calculator grid grid-cols-4 gap-2 shadow-xl bg-gray-300 text-black p-5 max-w-lg m-auto">
  <div class="text-right col-span-4 font-bold text-3xl m-5 ">{{current || '0'}}</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="percent">%</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="clearRecent">CE</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="clear">C</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="del">BackSpace</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="reverse">1/x</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="power">x^2</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="sqrt">x^0.5</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="divide">/</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(7)">7</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(8)">8</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(9)">9</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="time">X</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(4)">4</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(5)">5</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(6)">6</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="minus">-</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(1)">1</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(2)">2</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(3)">3</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-400 hover:bg-gray-600 hover:border-black" @click="add">+</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="sign">+/-</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="append(0)">0</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-gray-200 hover:bg-gray-600 hover:border-black" @click="dot">.</div>
  <div class="align-text-bottom inline-block border-solid border-transparent border-2 bg-blue-300 hover:bg-blue-500 hover:border-blue-600" @click="equal">=</div>
</div>
</template>

<script>
export default {
  name: 'Calculator',
  data(){
    return{
       current : '',
      prev: null,
      operator: null,
      operatorClicked: false
    }
  },
  methods:{
    clear(){
      this.current = '';
      this.prev = null;
    },
    clearRecent(){
      this.current = '';
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
    },
    percent(){
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number){
      if (this.operatorClicked){
        this.current=''
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot(){
      if (this.current.indexOf('.') === -1){
        this.append('.')
      }
    },

    setPrevious(){
      this.prev = this.current
      this.operatorClicked = true
    },
    divide(){
      this.operator = (a,b) => a/b
      this.setPrevious()
    },
    minus(){
      this.operator = (a,b) => a-b
      this.setPrevious()
    },
    add(){
      this.operator = (a,b) => a+b
      this.setPrevious()
    },
    times(){
      this.operator = (a,b) => a*b
      this.setPrevious()
    },
    equal(){

    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  grid-auto-rows: minmax(50px, auto);
}

</style>
