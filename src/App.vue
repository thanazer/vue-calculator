<template>
  <div id="app">
    <b-container>
      <b-row>
        <b-col sm="6" offset-sm="4">
          <Calculator />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Calculator from './components/Calculator';

export default {
  name: 'App',
  components: {
    Calculator,
  },
};
</script>
