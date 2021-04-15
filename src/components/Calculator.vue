<template>
    <div class = "calculator">
        <div class = "result">{{current}} </div>
            <button @click="clean" class="gray">AC</button>
            <button @click="change" class="gray">+/-</button>
            <button @click="del" class="gray">DEL</button>
            <button @click="operator('/')" class="orange">/</button>
            <button @click="appear('7')">7</button>
            <button @click="appear('8')">8</button>
            <button @click="appear('9')">9</button>
            <button @click="operator('*')" class="orange">x</button>
            <button @click="appear('4')">4</button>
            <button @click="appear('5')">5</button>
            <button @click="appear('6')">6</button>
            <button @click="operator('-')" class="orange">-</button>
            <button @click="appear('1')">1</button>
            <button @click="appear('2')">2</button>
            <button @click="appear('3')">3</button>
            <button @click="operator('+')" class="orange">+</button>
            <button @click="appear('0')" class="zero">0</button>
            <button @click="dot()">.</button>
            <button @click="equal('eq')" class="orange">=</button>
        </div>

</template>

<script>
export default {
     data(){
    return{
      current: 0,
      ap : 0
      }
    },


    methods : {
        clean() {
            this.current = "0";
            this.result = this.current;
        },
        change() {
      this.current = this.current.charAt(0) === '-' ? 
      this.current.slice(1) : `-${this.current}`; 
    },
           del() {
      this.current = this.current.slice(0,-1);
      if(this.current.length <= 0)  [
          this.current = "0"
      ]
    },

        appear(num) {
      if(this.ap == 1){
        this.ap = 0 ;
        
      }
      console.log(this.current)
      if(this.current == "0"){
          this.current = num
      }
      else this.current += num
    },
         operator(operate){
             if(this.ap == 1) {
             this.current = this.current.slice(0,-1);
             this.current += operate;
             }
      else this.current += operate; 
      this.ap = 1;
    },       

        dot() {
            var temp = ""
            for(var i = this.current.length-1;i>=0;i--){
                if(this.current[i]=='+' || this.current[i]=='-' ||this.current[i]=='*' ||this.current[i]=='/' ){
                    break
                }
                temp = this.current[i] + temp
            }
            if(temp.indexOf('.') === -1) {
                this.appear('.');
            }
        },
        equal() {
            this.current = ''+eval(this.current);     
        }
       
    }
}
</script>

<style>
.calculator{
  margin:auto;
  width: 300px;
  height: 375px;
  font-size: 20px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  border-radius: 1em;
  border: 3px solid black;
  background-color: black;
  
}

.button {
    display : grid;
    grid-template-columns: repeat(4, 1fr);
}

.zero {
    grid-column: 1/3;
}

* {
    box-sizing: border-box;
    color: white;
}
.result{
    color : white;
    grid-column: 1 / 5;
    margin-top: 4%;
    margin-bottom: 7%;
    text-align: right;

}
input, button {
    height: 60px;
    outline: none;
    background: gray;
    border-radius: 1em;
}
input {
    width: 100%;
    text-align: right;
    border: none;
    background: black;
    padding-right: 1rem;
    font-size: 2rem;
}
.orange{
    background: rgb(233, 109, 8);
}
.gray{
    background: rgb(218, 216, 216);
    color : black;
    font-weight: bold;
}
</style>