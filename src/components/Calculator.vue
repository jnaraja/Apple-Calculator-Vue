<template>
    <div class="backdrop">
        <card>
            <div>
                <input type="text" v-model="number"
                    oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*)\./g, '$1');" />
            </div>
            <div>
                <button @click="clear">{{ clearText }}</button>
                <button @click="oppo">+/-</button>
                <button @click="percent">%</button>
                <button @click="divide" class="operations">/</button>
            </div>
            <div>
                <button class="numbers-dot" @click="numberPressed(7)">7</button>
                <button class="numbers-dot" @click="numberPressed(8)">8</button>
                <button class="numbers-dot" @click="numberPressed(9)">9</button>
                <button @click="multiply" class="operations">x</button>
            </div>
            <div>
                <button class="numbers-dot" @click="numberPressed(4)">4</button>
                <button class="numbers-dot" @click="numberPressed(5)">5</button>
                <button class="numbers-dot" @click="numberPressed(6)">6</button>
                <button @click="subtract" class="operations">-</button>
            </div>
            <div>
                <button class="numbers-dot" @click="numberPressed(1)">1</button>
                <button class="numbers-dot" @click="numberPressed(2)">2</button>
                <button class="numbers-dot" @click="numberPressed(3)">3</button>
                <button class="operations" @click="add">+</button>
            </div>
            <div>
                <button class="zero" @click="numberPressed(0)">0</button>
                <button class="numbers-dot" @click="decimal">.</button>
                <button class="operations" @click="equals">=</button>
            </div>
        </card>
    </div>

</template>

<script>
export default {
    data() {
        return {
            number: 0,
            results: 0,
            clearText: "AC",
            newNumber: false,
            addition: false,
            subtraction: false,
            division: false,
            multiplication: false,
        }
    },

    methods: {
        clear(clearText) {
            this.number = 0;
            this.clearText = "AC";
            this.addition = false;
            this.subtraction = false;
            this.division = false;
            this.multiplication = false;
            this.newNumber = false;
        },
        numberPressed(num) {
            this.clearText = "C";
            if (this.newNumber == true) {
                this.newNumber = false;
                this.number = num;
            } else {
                this.number = (this.number * 10) + num;
            }

        },

        add() {
            this.newNumber = true;
            this.addition = true;
            this.subtraction = false;
            this.division = false;
            this.multiplication = false;
            this.results = this.number;
        },

        subtract() {
            this.newNumber = true;
            this.addition = false;
            this.subtraction = true;
            this.division = false;
            this.multiplication = false;
            this.results = this.number;
        },

        divide() {
            this.newNumber = true;
            this.addition = false;
            this.subtraction = false;
            this.division = true;
            this.multiplication = false;
            this.results = this.number;
        },

        multiply() {
            this.newNumber = true;
            this.addition = false;
            this.subtraction = false;
            this.division = false;
            this.multiplication = true;
            this.results = this.number;
        },

        oppo() {
            this.number *= -1;
        },

        decimal() {
            // TODO: add decimals to input
        },

        percent() {
            this.number /= 100; 
        },

        equals() {
            if (this.addition == true) {
                this.number += this.results;
            }
            if (this.subtraction == true) {
                this.number = this.results - this.number;
            }
            if (this.division == true) {
                this.number = this.results/this.number;
            }
            if (this.multiplication == true) {
                this.number *= this.results;
            }
            this.newNumber = true;
        }
    }
}
</script>

<style>
@import '../assets/main.css';
</style>