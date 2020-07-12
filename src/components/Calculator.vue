<template>
  <b-card align="center" class="mt-4 p-0">
    <div class="output-screen p-2 d-flex align-items-center">
      {{ secondOperand || firstOperand || 0 }}
    </div>
    <div class="button-container">
      <b-row no-gutters>
        <b-col>
          <b-button block variant="warning">C</b-button>
        </b-col>
      </b-row>
      <b-row no-gutters>
        <b-button>7</b-button>
        <b-button>8</b-button>
        <b-button>9</b-button>
        <b-button variant="warning">+</b-button>
      </b-row>
      <b-row no-gutters>
        <b-button>4</b-button>
        <b-button>5</b-button>
        <b-button>6</b-button>
        <b-button variant="warning">-</b-button>
      </b-row>
      <b-row no-gutters>
        <b-button>1</b-button>
        <b-button>2</b-button>
        <b-button>3</b-button>
        <b-button variant="warning">*</b-button>
      </b-row>
      <b-row no-gutters>
        <b-button>0</b-button>
        <b-button>.</b-button>
        <b-button>=</b-button>
        <b-button variant="warning">/</b-button>
      </b-row>
    </div>
  </b-card>
</template>

<script>
export default {
  name: 'Calculator',
  data() {
    return {
      firstOperand: '',
      secondOperand: '',
      operator: '',
    };
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
</style>
