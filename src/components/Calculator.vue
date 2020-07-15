<template>
  <b-card align="center" class="mt-4 p-0">
    <div class="output-screen p-2 d-flex align-items-center">{{ screenValue }}</div>
    <div class="button-container">
      <b-row no-gutters>
        <b-col>
          <b-button @click="allClear()" v-if="clearUsed" block variant="warning">AC</b-button>
          <b-button @click="clear()" v-else block variant="warning">C</b-button>
        </b-col>
      </b-row>
      <b-row no-gutters>
        <b-button @click="numberClicked(7)">7</b-button>
        <b-button @click="numberClicked(8)">8</b-button>
        <b-button @click="numberClicked(9)">9</b-button>
        <b-button variant="warning" @click="operatorClicked('+')">+</b-button>
      </b-row>
      <b-row no-gutters>
        <b-button @click="numberClicked(4)">4</b-button>
        <b-button @click="numberClicked(5)">5</b-button>
        <b-button @click="numberClicked(6)">6</b-button>
        <b-button variant="warning" @click="operatorClicked('-')">-</b-button>
      </b-row>
      <b-row no-gutters>
        <b-button @click="numberClicked(1)">1</b-button>
        <b-button @click="numberClicked(2)">2</b-button>
        <b-button @click="numberClicked(3)">3</b-button>
        <b-button variant="warning" @click="operatorClicked('*')">*</b-button>
      </b-row>
      <b-row no-gutters>
        <b-button @click="numberClicked(0)">0</b-button>
        <b-button @click="numberClicked('.')">.</b-button>
        <b-button @click="equalsClicked()">=</b-button>
        <b-button variant="warning" @click="operatorClicked('/')">/</b-button>
      </b-row>
    </div>
  </b-card>
</template>

<script>
import { evaluate } from 'mathjs';

export default {
  name: 'Calculator',
  data() {
    return {
      firstOperand: '',
      secondOperand: '',
      operator: '',
      clearUsed: true,
      currentOperand: 'firstOperand',
    };
  },
  computed: {
    screenValue: function() {
      if (
        this.currentOperand === 'secondOperand' &&
        this.secondOperand === ''
      ) {
        return this.firstOperand;
      } else {
        return this[this.currentOperand];
      }
    },
  },
  methods: {
    numberClicked(num) {
      this.clearUsed = false;
      if (num === '.' && this[this.currentOperand] === '') {
        this[this.currentOperand] += '0.';
      } else if (num === '.' && !this[this.currentOperand].includes('.')) {
        this[this.currentOperand] += num;
      } else if (num !== '.') {
        this[this.currentOperand] += num;
      }
    },
    operatorClicked(op) {
      this.currentOperand = 'secondOperand';
      if (this.firstOperand !== '' && this.secondOperand == '') {
        this.operator = op;
      } else if (this.firstOperand !== '' && this.secondOperand !== '') {
        this.firstOperand = evaluate(
          this.firstOperand + this.operator + this.secondOperand
        ).toString();
        this.secondOperand = '';
        this.operator = op;
      }
    },
    equalsClicked() {
      this.firstOperand = evaluate(
        this.firstOperand + this.operator + this.secondOperand
      ).toString();
      this.secondOperand = '';
      this.operator = '';
      this.currentOperand = 'firstOperand';
    },
    clear() {
      this[this.currentOperand] = '';
      this.clearUsed = true;
    },
    allClear() {
      this.firstOperand = '';
      this.secondOperand = '';
      this.operator = '';
      this.currentOperand = 'firstOperand';
    },
  },
};
</script>

<style lang="scss" scoped>
//TODO: Add nice border around the card to get a bessel.
$orange: #ffc107;
$dark-gray: #6c757d;

.output-screen {
  height: 60px;
  border: 1px solid #000;
  text-align: right;
}

.card {
  width: 242px;
  border: 1px solid #000;
  border-radius: 0;
}

.card-body {
  padding: 0;
}

.btn {
  width: 60px;
  height: 60px;
  border: 1px solid #000;
  border-radius: 0;
  background-color: $dark-gray;
  &.btn-block {
    width: 100%;
  }
  &:hover {
    border: 1px solid #000;
    background-color: darken($color: $dark-gray, $amount: 8%);
  }
}

.btn-warning {
  background-color: $orange;
  &:hover {
    background-color: darken($color: $orange, $amount: 8%);
  }
}

.btn:focus,
.btn:active {
  outline: none !important;
  box-shadow: none;
  border: 1px solid #000;
}
</style>
