<template>
  <base-button
    @click.native="emitEventTwo"
  >
    Emit from Child Two
  </base-button>
</template>

<script>
import BaseButton from '@/components/button/base-button.vue'
export default {
  components: {
    BaseButton
  },
  props: {
    parentMessageTwo: {
      type: Function,
      default: null
    }
  },
  data () {
    return {
      payload: {
        title: 'Payload from Child Two',
        body: 'This message is emitted from child component two. \n Clicking "Okay" will pass a function to the child component that will in turn execute it.'
      }
    }
  },
  watch: {
    parentMessageTwo (newVal, oldVal) {
      console.log('new value from parent')
      if (typeof newVal === 'function') {
        this.callFunction(newVal)
      } else {
        this.emitEventTwo({
          title: '🔴 Expected Function',
          body: `Child component expected a prop of type 'function'. You passed a(n) ${typeof newVal}`
        })
      }
    }
  },
  methods: {
    // Emits `modal` event to parent
    emitEventTwo ($event, payload) {
      if (payload) {
        console.log(payload)
        this.$emit('modal', payload)
      } else this.$emit('modal', this.payload)
    },
    // Calls function passed as argument
    callFunction (fn) {
      console.log('calling function')
      fn()
    }
  }
}
</script>
