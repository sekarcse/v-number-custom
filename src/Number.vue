<template>
  <input :id="id"
         ref="ref1" 
         :placeholder="placeholder"
         :value="value"
         :tabindex="tabindex"
         :min="min"
         :max="max"
         :style="width"
         class="input"
         type="number"
         @keyup="filterInput($event)"
         @input="filterInput($event)"
         @paste.prevent
  >
</template>

<script>

export default {
  name: 'vue-number-custom',
  props: {
    id: {
      type: String,
      required: false,
      default: null
    },
    placeholder: {
      type: String,
      required: false,
      default: ''
    },
    value: {
      type: [ Number, String ],
      required: false,
      default: null
    },
    min: {
      type: Number,
      required: false,
      default: null
    },
    max: {
      type: Number,
      required: false,
      default: null
    },
    tabindex: {
      type: Number,
      required: false,
      default: null
    },
    precision: {
      type: Number,
      required: false,
      default: 2
    },
    width: {
      type: String,
      required: false,
      default: ''
    }
  },

  data () {
    return {
      oldValue: this.value,
      pattern: this.getPattern(),
      allowedChars: [ '1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '.', '-' ]
    }
  },

  methods: {
    filterInput (e){
      if ([ '.', 'e' ].includes(e.data) && isNaN(e.target.valueAsNumber)) {
        this.updateVal(0)
        e.preventDefault()
        return
      }
      if (e.data === 'e' || (this.allowedChars.includes(e.data) && !this.isValid(e.target.value))) {
        this.updateVal(this.oldValue)
        e.preventDefault()
        return
      } 
      if (this.pattern.test(e.target.value)) {
        this.oldValue = parseFloat(e.target.value)
        this.$emit('input', this.oldValue)
      } else {
        if (e.target.value === '') {
          this.oldValue = null
        }
        this.updateVal(this.oldValue)
      }
    },

    isValid (value) {
      if (value === '') {
        return false
      } else {
        const val = parseFloat(value) || null
        if (value === null || 
           (this.min !== null && value < this.min) || 
           (this.max !== null && value > this.max)) {
          return false 
        } else {
          return true
        }
      }
    },

    updateVal (value) {
      this.$emit('input', value)
      this.$forceUpdate()
    },

    getPattern () {
      switch (this.precision) {
        case 1:
          return /^-?\d+(\.\d{1,1})?$/
        case 2:
          return /^-?\d+(\.\d{1,2})?$/
        case 3:
          return /^-?\d+(\.\d{1,3})?$/
        case 4:
          return /^-?\d+(\.\d{1,4})?$/
        case 5:
          return /^-?\d+(\.\d{1,5})?$/
        case 6:
          return /^-?\d+(\.\d{1,6})?$/
        case 7:
          return /^-?\d+(\.\d{1,7})?$/
        case 8:
          return /^-?\d+(\.\d{1,8})?$/
        default:
          return /^-?\d*$/
      }
    }
  }
}

</script>
