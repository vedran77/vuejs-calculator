<template>
    <div class="calculator">
        <div class="display"><p><span>{{this.subResult}}</span><br>{{this.result}}</p></div> 
        <Operation @click="this.clear();" :operation="'C'"/>
        <Operation @click="this.clearAll();" :operation="'CE'"/>
        <Operation @click="this.sing();" :operation="'+/-'"/>
        <Operation @click="this.divide();" :operation="'/'"/>
        <Number @click="this.appendNumber(7);" :number="7"/>
        <Number @click="this.appendNumber(8);" :number="8"/>
        <Number @click="this.appendNumber(9);" :number="9"/>
        <Operation @click="this.multiply();" :operation="'X'"/>
        <Number @click="this.appendNumber(4);" :number="4"/>
        <Number @click="this.appendNumber(5);" :number="5"/>
        <Number @click="this.appendNumber(6);" :number="6"/>
        <Operation @click="this.subtraction();" :operation="'-'"/>
        <Number @click="this.appendNumber(1);" :number="1"/>
        <Number @click="this.appendNumber(2);" :number="2"/>
        <Number @click="this.appendNumber(3);" :number="3"/>
        <Operation @click="this.sum();" :operation="'+'"/>
        <div @click="this.appendNumber(0);" class="zero"><p>0</p></div>
        <Operation @click="this.calculate();" :operation="'='"/>
    </div> 
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

import Number from './Number.vue';
import Operation from './Operation.vue';

@Options({
  components: {
    Number,
    Operation
  },
})

export default class Calculator extends Vue {
    public result: string = "0";
    public subResult: string = "0";
    public operation: number = 0;

    public clear(): void {
        this.result = "0";
    }

    public sing(): void {
        if (this.result === '0') {
            return;
        }

        const result: number = parseInt(this.result);

        if (result < 0) {
            this.result = `${-result}`;
        } else {
            this.result = `-${this.result}`;
        }
    }

    public clearAll(): void {
        this.result = "0";
        this.subResult = "0";

        this.operation = 0;
    }

    public appendNumber(num: number) {
        if (this.result === "0") {
            this.result = num.toString();

            return;
        }

        if (this.result.length >= 15) {
            return;
        }

        this.result += num.toString();
    }

    public divide(): void {
        this.subResult = this.result += " / ";
        this.result = "0";

        this.operation = 1;
    }

    public multiply(): void {
        this.subResult = this.result += " x ";
        this.result = "0";

        this.operation = 2;
    }

    public subtraction(): void {
        this.subResult = this.result += " - ";
        this.result = "0";

        this.operation = 3;
    }

    public sum(): void {
        this.subResult = this.result += " + ";
        this.result = "0";

        this.operation = 4;
    }

    public calculate(): void {
        if (this.operation === 0) {
            return;
        }

        const numberOne: number = parseInt(this.subResult);
        const numberTwo: number = parseInt(this.result); 
        let result: number = 0;

        switch (this.operation) {
            case 1: {
                result = numberOne / numberTwo;
                break;
            }

            case 2: {
                result = numberOne * numberTwo;
                break;
            }

            case 3: {
                result = numberOne - numberTwo;
                break;
            }

            case 4: {
                result = numberOne + numberTwo;
                break;
            }
        }

        this.subResult = `${this.subResult}${this.result}`;
        this.result = result.toString();

        if (this.result.length > 15) {
            this.result = "Error";
        }

        this.operation = 0;
    }
}
</script>

<style scoped>
.calculator {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: grid;
    grid-template-columns: repeat(4, 70px);
    grid-auto-rows: minmax(50px, auto);
    border-radius: 10px;
    color: #000;
}

.display {
    grid-column: 1 / 5;
    text-align: right;
    background: #151515;
    border-radius: 10px 10px 0px 0px;
}

.display p {
    padding-right: 10px;
    font-family: 'Nunito', sans-serif;
    font-size: 24px;
    color: #fff;
    font-weight: bold;
}

.display p span {
    font-size: 13px;
    color: #888;
}

.zero {
    grid-column: 1 / 4;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #ebe7e4;
    z-index: -1;
}

.zero:hover {
    cursor: pointer;
}

</style>
