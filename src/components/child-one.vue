<template>
  <div class="child-one">
    <base-button
    @click.native="emitEventOne"
    >
      Emit from Child One
    </base-button>
    <p>{{ parentMessageOne }}</p>
  </div>
</template>

<script>
import BaseButton from '@/components/button/base-button.vue'
export default {
  components: {
    BaseButton
  },
  props: {
    parentMessageOne: {
      default: null
    }
  },
  methods: {
    emitEventOne () {
      const payload = {
        title: 'Payload from Child One',
        body: 'This message is emitted from child component one',
        buttonMessage: 'Got it!'
      }
      this.$emit('modal', payload)
    }
  }
}
</script>
