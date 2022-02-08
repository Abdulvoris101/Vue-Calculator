<template>
  <div id="app">
    <div class="wrapper">
      <div class="">
        <input type="text" class="output ps-3 input-output" @keyup.enter="calc()" v-model="result" @input="validateOutput">
      </div>
      <div class="operators row ">
        <div class="button-group  col-lg-3 mb-3 col-sm-3"
         v-for="(operator, index) in operators"
        :key="index">
          <button class=" ms-1 button-operator"
          @click="input(operator)">
            {{ operator }}
          </button>
        </div>
        <main class="main row ms-1">
          <div 
          class="numbers col-lg-11 gx-5 row">
             <div class="row ">
                <button  
                  v-for="(number, index) in numbers" :key="index" 
                  @click="input(number)"
                  class="col-lg-4  mb-1 btn-number"
                  >
                  {{ number }}  
                </button>
                <button @click="reset" class="btn-number">
                  C
                </button>
                {{ validation.error }}
                

             </div>
          </div>
           <div class="equally-button col-lg-1" @click="calc">
            <button class="btn btn-primary  btn-large "> {{ quality }} </button>
          </div>
        </main>
      </div>
    </div>  
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data() {
    return {
      operators: ['+', '/', '*', '-'],
      numbers: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      quality: '=',
      result: '0',
      validation: {
        alphabet: 'abcdefghijklmnopqrstuvwxyz'.split(''),
        error: '',  
        symbols: '!~|@#$^&'.split('')
      }
    }
  },
  created() {
    this.reverseNumber()
  },
  methods: {
    reverseNumber() {
      return this.numbers.reverse()
    },
    input(char) {
      this.result = this.result.toString()
      this.result += char
    },
    reset() {
      this.result = ''
    },
    calc() {
      this.result = eval(this.result)
    },
    validateOutput(event) {
      let length = this.validation.alphabet.length
      let value = event.data
      
        for (let i = 0; i < length; i++) {
          if (value == this.validation.alphabet[i]) {
            this.result = ''
          }
        }
    }
    
    
    
  },
  watch: {
      result(currentValue) {
        let length = this.validation.alphabet.length
        let symbols = this.validation.symbols
        this.operators.length = 3;
        
        for (let i = 0; i < length; i++) {
          console.log(this.operators[i]);
          if (currentValue == this.operators[i] || currentValue == symbols[i]) {
            this.result = ''
          }
        }
        this.operators.push('-')
      }
    }
}
</script>

<style lang="scss">
.wrapper {
  margin: 50px auto;
  width: 550px;
  padding: 30px;
  border: 2px solid #ccc;

}
.output {
  margin: 0 auto;
  height: 50px;
  margin-bottom: 20px;
  border: 2px solid #ccc;
}
.output:hover {
  box-shadow: -1px -1px 9px -6px rgba(34, 60, 80, 0.6) inset;
}

.button-operator {
  padding: 14px 35px;
  background: #f5f5f5;
  border: 1px solid rgb(241, 241, 241);
  border-radius: 3px;
}
.operators {
  margin-left: auto;
  margin-right: auto;
}
.button-operator:hover {
  border-color: #949393 !important;
}
.button-operator:active {
  background-color: #525252 !important;
  color: #fff;
}
.btn-number {
  padding: 10px 0;
  background: #f5f5f5;
  border: 1px solid rgb(255, 255, 255);
}
.btn-number:hover {
  border-color: #949393;
}
.btn-number:active {
  background-color: #525252 !important;
  color: #fff;
}
.btn-number:focus {
  background: #afafaf !important;
}
.btn-large {
  padding: 30px 12px;
}
.btn-large:focus {
  box-shadow: none !important;
}
.input-output {
  width: 100%;
  display: block;
  outline: none;
}

</style>
