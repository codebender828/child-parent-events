<template>
    <transition name="modal">
        <div v-show="showModal" class="mask">
            <div class="wrapper">
                <div class="container">
                  <div class="default">
                    <slot name="default" />
                  </div>

                  <div class="header">
                    <slot name="header" />
                  </div>

                  <div class="body">
                    <slot name="body" />
                  </div>

                  <div class="action">
                    <slot name="footer" />
                  </div>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
export default {
  name: 'Modal',
  props: {
    showModal: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {}
  }
}
</script>

<style lang="scss" scoped>
.mask {
  width: 100%;
  height: 100%;
  position: fixed;
  display: flex;
  background-color: rgba(0, 0, 0, 0.5);
  font-size: 16px;
  font-family: var(--rubik);
  transition: opacity 0.3s ease;
  z-index: 9998;
  top: 0;
  left: 0;
  place-items: center center;

  .wrapper {
    width: 100%;
    height: 100%;
    display: flex;
    vertical-align: middle;
    place-items: center center;

    .container {
      width: fit-content;
      height: fit-content;
      margin: 0 auto;
      padding: 20px 20px;
      position: relative;
      display: flex;
      z-index: 1;
      flex-direction: column;
      background-color: var(--white);
      transition: all 0.3s ease;
      border-radius: 5px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
      max-width: 350px;

      .default {
        font-size: 1em;
        font-weight: 300;
      }

      .header {
        margin: 0;
        display: flex;
        flex-direction: row;
        align-items: center;

        h1,
        h2,
        h3,
        h4,
        h5,
        h6 {
          font-size: 1.3em;
        }
      }

      .body {
        margin: 20px 0;
        font-size: 1em;
        font-weight: 300;
        overflow-wrap: break-word;

        p {
          margin: 0;
        }
      }

      .action {
        height: auto;
        margin-bottom: 10px;
        display: flex;
      }
    }
  }
}

/*
* The following styles are auto-applied to elements with
* transition="modal" when their visibility is toggled
* by Vue.js.
*
* You can easily play with the modal transition by editing
* these styles.
*/

.modal-enter-active {
  transition: opacity 0.2s ease-in;
}

.modal-leave-active {
  transition: opacity 0.2s ease-out;
}

.modal-enter,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.1);
}

.modal-leave,
.modal-enter-to {
  opacity: 1;
  transform: scale(1.1);
}

</style>
