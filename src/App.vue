<template>
  <div id="app">
    <p>Child components<code class="code">ChildOne</code> and <code class="code">ChildTwo</code> both emit the same <code class="code">modal</code> event to the <code class="code">App.vue</code> parent component. </p>
    <p>The <code class="code">App</code> parent component has one <code class="code">Modal</code> component that is shown by the parent when it received the event to show the modal.</p>
    <p>They however have separate handlers because I have explicitly declared that they do so.</p>
    <div class="wrapper">
      <child-one :parent-message-one="dataOne" @modal="handleEventOne" class="child" />
      <child-two :parent-message-two="dataTwo" @modal="handleEventTwo" class="child" />
    </div>
    <p>{{ parentMessage }}</p>
    <modal :show-modal="showModal">
      <h1 slot="header">{{ modalMessage.title }}</h1>
      <p slot="body">{{ modalMessage.body }}</p>
      <div slot="footer">
        <base-button
          @click.native="removeModal"
        >
          {{ modalMessage.buttonMessage ? modalMessage.buttonMessage : 'Okay' }}
        </base-button>
        <base-button
          button-type="warning"
          v-if="showFuncButton"
          @click.native="passFuncToChild"
        >
          Pass function from parent to child
        </base-button>
      </div>
    </modal>
  </div>
</template>

<script>
import ChildOne from '@/components/child-one.vue'
import ChildTwo from '@/components/child-two.vue'
import BaseButton from '@/components/button/base-button.vue'
import Modal from '@/components/modal/modal.vue'

export default {
  name: 'App',
  components: {
    BaseButton,
    Modal,
    ChildOne,
    ChildTwo
  },
  data () {
    return {
      modalMessage: {},
      showModal: false,
      dataOne: undefined,
      dataTwo: undefined,
      parentMessage: null,
      showFuncButton: false
    }
  },
  methods: {
    parentFunction () {
      this.removeModal()
      this.parentMessage = '🎉 Function called by a child component'
    },
    removeModal () {
      this.showModal = false
    },
    handleEventOne (message) {
      this.modalMessage = message
      this.showModal = true
      this.dataOne = 'Message passed to child one from parent'
    },
    handleEventTwo (message) {
      this.modalMessage = message
      this.showModal = true
      this.showFuncButton = true
    },
    passFuncToChild () {
      this.dataTwo = this.parentFunction
    }
  }
}
</script>

<style lang="scss">
html {
  font-size: 16px;
}

body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.wrapper {
  display: flex;
  justify-content: space-evenly;
}

.code {
  background: var(--light);
  padding: 5px;
  border-radius: 5px;
}

</style>
