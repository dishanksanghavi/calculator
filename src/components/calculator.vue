<template>
  <div class = "calculator">
    <transition name="slide-fade">
      <div class = "display" v-if="answer !== ''" v-cloak >{{answer}}</div>
    </transition>
    <div class="display" v-cloak >{{ logList + current }}</div>
    <div @click = "clear" class = "btn top">Clear</div>
    <div @click = "sign" class = "btn top">+/-</div>
    <div @click = "percent" class = "btn top">%</div>
    <div @click = "divide" class = "btn right">/</div>
    <div @click = "append('7')" class = "btn">7</div>
    <div @click = "append('8')" class = "btn">8</div>
    <div @click = "append('9')" class = "btn">9</div>
    <div @click = "times" class = "btn right">X</div>
    <div @click = "append('4')" class = "btn">4</div>
    <div @click = "append('5')" class = "btn">5</div>
    <div @click = "append('6')" class = "btn">6</div>
    <div @click = "minus" class = "btn right">-</div>
    <div @click = "append('1')" class = "btn">1</div>
    <div @click = "append('2')" class = "btn">2</div>
    <div @click = "append('3')" class = "btn">3</div>
    <div @click = "add" class = "btn right">+</div>
    <div @click = "append('0')" class = "zero btn">0</div>
    <div @click = "dot" class = "btn">.</div>
    <div @click = "equal" class = "btn right">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      logList: "",
      current: "",
      answer: "",
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = "";
			this.answer = "";
			this.logList = "";
			this.operatorClicked = false;
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      if (this.answer != "") {
				this.answer = `${parseFloat(this.answer) / 100}`;
			}
      else {
        this.current = `${parseFloat(this.current) / 100}`;
      }
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    addtoLog(operator) {
			if (this.operatorClicked == false) {
				this.logList += `${this.current} ${operator} `;
				this.current = "";
				this.operatorClicked = true;
			}
		},
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    divide() {
      this.addtoLog("/");
    },
    times() {
      this.addtoLog("X");
    },
    minus() {
      this.addtoLog("-");
    },
    add() {
      this.addtoLog("+");
    },
    equal() {
      if (this.operatorClicked == false) {
				this.answer = eval(this.logList + this.current);
			} 
      else {
				this.answer = "WHAT?!!";
			}
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
[v-cloak] { display: none; }
.display {
  color: white;
  background-color: black;
  grid-column: 1/5;
}
.calculator {
  width: 450px;
  margin: 0 auto;
  font-size: 35px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  background-color: black;;
}
.zero {
  grid-column: 1/3;
}
.btn {
  border: none;
  background-color: grey;
  text-align: center;
  cursor: pointer;
  border-radius: 50%;
  color: white;
  padding-top: 5px ;
}
.top {
  color: black;
  background-color: lightgrey;
}
.right {
  background-color: orange;
}
</style>
