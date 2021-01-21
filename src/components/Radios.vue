<template>
  <div class="radios">
    <div v-for="(option, idx) in options" :key="`l-${idx}`" :class="inputClass">
      <input
        type="radio"
        :id="id + idx"
        :name="`radio-${idx}`" 
        :value="option"
        :checked="option === defaultValue"
        :disabled="disabled"
        @change="update(option, idx)"
      /> 
      <span :class="option === defaultValue ? 'checkmark checked' : 'checkmark'"></span>     
      <label :for="id + idx">{{ option }}</label>
      
    </div>
  </div>
</template>

<script>
export default {
  name: "Radios",
  props: {
    id: {
      type: String,
      required: true
    },
    defaultValue: {
      type: [String, Number, Boolean, Object],
      default: null
    },
    options: {
      type: Array,
      required: true
    },
    inputClass: {
      type: [String, Object],
      default: ""
    },
    disabled: {
      type: Boolean,
      default: false,
    }
  },
  data() {
    return {
      indexSelected: null
    }
  },
  methods: {
    update(value, idx) {
      this.indexSelected = idx;
      this.$emit("change", { value: value, id: this.id });
    }
  }
};
</script>

<style scoped>
*,
*:before,
*:after {
  box-sizing: border-box;
}
.radios {
  width: 260px;
}
@media only screen and (max-width: 800px) {
  .radios {
    width: 50vw;
  }
}
.radios label {
  padding-left: 40px;
}
.radios > div {
  margin: 10px 0px;
  position: relative;
}
.radios > div:not(:last-child) {
  border-bottom: solid 1px #bbb;
  padding-bottom: 8px;
}

/* https://www.w3schools.com/howto/tryit.asp?filename=tryhow_css_custom_radio */

/* Hide the browser's default radio button */
.radios > div input {
  position: absolute;
  opacity: 0;
}
/* Create a custom radio button */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 20px;
  width: 20px;
  border: 1px solid #bbb;
  border-radius: 50%;
  pointer-events: none; /* stopPropagation() */
}
/* Style the indicator (dot/circle) */
/*
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
 	top: 9px;
	left: 9px;
	width: 8px;
	height: 8px;
	border-radius: 50%;
	background: white;
}
*/

/* On mouse-over, add a grey background color */
.radios > div:hover input ~ .checkmark {
  border: 1px solid #032a43;
}

/* When the radio button is checked, add a blue background */
input:checked ~ .checkmark,
.checkmark.checked {
  background-color: #032a43;
}
input:checked ~ label {
  color: #032a43;
  font-weight: bold;
}
/* Show the indicator (dot/circle) when checked */
input:checked ~ .checkmark:after {
  display: block;
}
</style>