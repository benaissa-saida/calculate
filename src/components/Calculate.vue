<template>
    <div class="calculator">
        <div class="middle">
            <!-- <small v-if="selectedOperation">{{ prevNum }} {{ selectedOperation }} {{ currentNum }}</small> -->
            <div>
                <h1>{{currentNum}}</h1>
            </div>
        </div>
        <div class="bottom">
            <button @click="pressed('c')">c</button>
            <button @click="negateValue">+/-</button>
            <button @click="pressed('%')">%</button>
            <button class="operator" @click="pressed('÷')">÷</button>

            <button @click="pressed('7')">7</button>
            <button @click="pressed('8')">8</button>
            <button @click="pressed('9')">9</button>
            <button class="operator" @click="pressed('*')">*</button>

            <button @click="pressed('4')">4</button>
            <button @click="pressed('5')">5</button>
            <button @click="pressed('6')">6</button>
            <button class="operator" @click="pressed('-')">-</button>

            <button @click="pressed('1')">1</button>
            <button @click="pressed('2')">2</button>
            <button @click="pressed('3')">3</button>
            <button class="operator" @click="pressed('+')">+</button>
            
            <button @click="pressed('0')">0</button>
            <button @click="pressed('.')">.</button>
            <button class="operator" @click="pressed('=')">=</button>
        </div>
    </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const operations = ["+", "-", "*", "÷", "%"];
    const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"];
    const currentNum = ref("");
    const prevNum = ref("");
    const operatorClicked = ref(false);
    const selectedOperation = ref("");
    const total = ref('')
    const pressed = (value) => {
        switch (value) {
            case '=' || 'Enter': 
                calculate()
            break;
            case '%':
                percentage()
            break;
            case 'c': 
                clear()
            break;
            case '.': 
                dot()
            break;
            
        }
        if (operations.includes(value)) applyOperation(value);
        else if (numbers.includes(value)) appendNumber(value);
    }
    const appendNumber = (value) => {
        if (operatorClicked.value){
            operatorClicked.value = false;
            currentNum.value = '';
        }
      currentNum.value = `${currentNum.value}${value}`;
    }
    const applyOperation = (value) => {
      calculate();
      prevNum.value = currentNum.value;
      operatorClicked.value = true;
      selectedOperation.value = value;
    }
    const calculate = () => {
      if (selectedOperation.value === "*") multiply();
      else if (selectedOperation.value === "÷") divide();
      else if (selectedOperation.value === "%") percentage();
      else if (selectedOperation.value === "-") subtract();
      else if (selectedOperation.value === "+") add();
      prevNum.value = "";
      selectedOperation.value = "";
    }
    const multiply = () => {
      currentNum.value = Math.round(prevNum.value * currentNum.value * 100) / 100;
      total.value = currentNum.value;
    }
    const divide = () => {
      currentNum.value = Math.round(prevNum.value / currentNum.value * 100) / 100;
      total.value = currentNum.value;
    }
    const percentage = () => {
      currentNum.value = currentNum.value / 100;
      total.value = currentNum.value;
    }
    const subtract = () => {
      currentNum.value = prevNum.value - currentNum.value;
      total.value = currentNum.value;
    }
    const add = () => {
      currentNum.value = +prevNum.value + +currentNum.value;
      total.value = currentNum.value;
    }
    const clear = () => {
     currentNum.value = ""
     prevNum.value = ""
     selectedOperation.value = ""
    }
    const dot = () => {
        if( currentNum.value.indexOf('.') === -1){
            return currentNum.value = `${currentNum.value}.`;
        }
    }
    const negateValue = () => {
        currentNum.value === '0.' ? `-${currentNum.value}` : '0.'
        currentNum.value = `${currentNum.value * -1}` 
    }
    const handleKeydown = (e) => {
        pressed(e.key);
    }
    return { currentNum, pressed, handleKeydown, selectedOperation, prevNum, negateValue, total};
  },
};
</script>

<style lang="scss" scoped>
    .calculator {
        background-color: #2c2b2b;
        width: 20rem;
        border-radius: 2rem;
        margin: auto;
        position: relative;
    }
    .middle {
        margin-bottom: 3rem;
        height: 6rem;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        & div{
            overflow-x: scroll;
            margin-top: 1rem;
        }
        & small{
            font-weight: bold;
            color: #9c9c9e;
            font-size: .75rem;
            padding-right: 0.5rem;
        }
        & h1 {
            color: white;
            font-size: 2.5rem;
            font-weight: 600;
            letter-spacing: -1px;
            padding-right: 36px;
        }
    }
    .bottom {
        background-color: #fff;
        padding: 1rem;
        border-radius: 2rem;
        font-size: 1.4rem;
        height: 23rem;
        display: grid;
        grid-template-columns: repeat(auto-fit,minmax(4rem,1fr));
        grid-gap: .3rem;
    }
    .bottom button {
        background-color: #858586;
        padding-top: 12px;
        border-radius: 1.5rem;
        font-size: 1.65rem;
        display: flex;
        justify-content: center;
        align-content: center;
        color: white;
        &:nth-child(1) {
            padding-top: 10px;
            background-color: #333232;
        } 
        &:nth-child(2) {
            background-color: #333232;
        } 
        &:nth-child(3) {
            background-color: #333232;
        } 
        &.operator{
            background-color: #fa7538;
            padding-top: 10px;
        }
        &:nth-child(17){
            grid-column: 1/3;
        }
    }
</style>




