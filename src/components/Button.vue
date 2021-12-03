<template>
  <div id="calculator-buttons" v-bind:class="{rdButton: buttonOption.isRd}">
      <button class="calc-button" 
              v-on:click=buttonPressed
              v-bind:class="{operatorButton: buttonOption.isOperator, otherButton: buttonOption.isOther,equalButton: buttonOption.isEqual,mathSymbolButton: buttonOption.isMathSymbol}">
               {{buttonOption.name}}
      </button>
  </div>
</template>

<script>
export default {
  name: 'calculator-buttons',
  props: {
      buttonOption: Object
  },
  methods:{
      buttonPressed: function(event){
          this.$emit('handle-press', event.target);
      }
  }
}
</script>