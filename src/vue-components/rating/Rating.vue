<template>
  <div class="quasar-rating" :class="{disabled: disable}">
    <i
      v-for="index in max"
      :class="{active: (!mouseModel && model >= index) || (mouseModel && mouseModel >= index)}"
      @click="set(index)"
      @mouseover="__setHoverValue(index)"
      @mouseout="mouseModel = 0"
    >{{ icon }}</i>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Number,
      default: 0,
      required: true
    },
    max: {
      type: Number,
      required: true
    },
    icon: {
      type: String,
      default: 'grade'
    },
    disable: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      mouseModel: 0
    }
  },
  computed: {
    model: {
      get () {
        return this.value
      },
      set (value) {
        if (this.value !== value) {
          this.$emit('input', value)
        }
      }
    }
  },
  methods: {
    set (value) {
      if (!this.disable) {
        this.model = Math.min(this.max, Math.max(1, parseInt(value, 10)))
      }
    },
    __setHoverValue (value) {
      if (!this.disable) {
        this.mouseModel = value
      }
    }
  }
}
</script>
