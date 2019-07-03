<template>
    <a v-if="isLink" :id="idName" ref="link" :href="hrefTo" :class="buttonClass" class="base-button">
        <template v-if="hasIcon">
            <img :src="iconSrc" class="base-button__icon" alt="img" srcset="">
        </template>
        <div class="base-button__text"> <slot /></div>
    </a>
    <button v-else :id="idName" ref="button" :class="buttonClass" :disabled="disabled" class="base-button">
        <template v-if="hasIcon">
          <spinner v-show="isLoading" />
          <img v-show="!isLoading" :src="iconSrc" class="base-button__icon" alt="img" srcset="">
        </template>
        <div class="base-button__text"> <slot /></div>
    </button>
</template>

<script>
import { addClass } from '@/helpers/utils'
import Spinner from '../spinner/spinner.vue'

export default {
  name: 'Button',
  components: {
    Spinner
  },
  props: {
    idName: {
      default: '',
      type: String
    },
    hasIcon: {
      default: false,
      type: Boolean
    },
    isLink: {
      default: false,
      type: Boolean
    },
    hrefTo: {
      default: null,
      type: String
    },
    iconSrc: {
      default: '',
      type: String
    },
    disabled: {
      type: Boolean,
      default: false
    },
    buttonText: {
      default: 'Button',
      type: String,
      required: false
    },
    buttonClass: {
      default: '',
      type: String
    },
    buttonType: {
      default: 'default',
      validator (value) {
        // The value must match one of these strings
        return value.match(/^(default|success|warning|danger|disabled)$/)
      }
    },
    isLoading: {
      type: Boolean,
      default: false
    }
  },

  data () {
    return {
      // Logging style colors.
      log: {
        success: '#28a745',
        warning: '#fd7e14',
        error: '#dc3545',
        default: '#0062ff'
      },
      hasButtonType: false
    }
  },

  created () {
    // Button type validation.
    if (this.buttonType && !this.buttonType.match(/^(default|success|warning|danger|disabled)$/)) {
      console.log(`%c BaseButton: Unexpected prop "button-type" of '${this.buttonType}'. Expected prop "button-type" of 'default', 'success', 'warning', 'danger' or 'disabled'.`, `color: ${this.log.error}`)
    } else {
      this.hasButtonType = true
    };

    // Button vs Link element validation.
    if (this.isLink && !this.hrefTo) {
      console.log('%c BaseButton: Expected button with "is-link=\'true\'" prop to have "href-to" attribute. Make sure your that your <base-button> has an "href-to" attribute', `color: ${this.log.error}`)
    };
  },
  mounted () {
    // Matches button type to base class.
    if (this.hasButtonType) {
      addClass(this.$refs.link || this.$refs.button, this.buttonType)
    };
  }
}
</script>

<style lang="scss">
.base-button {
  height: 35px;
  margin: 5px;
  padding: 8px 12px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
  font-weight: 300;
  border: none;
  box-shadow: var(--button-shadow-lt);
  transition: background 0.2s ease-in;
  outline: none;

  .base-button__icon {
    width: 18px;
    height: 18px;
    margin-right: 5px;
  }
}

.default {
  background: var(--akkadu-blue);

  &:hover {
    background: #007bff;
  }
}

.success {
  background: var(--success);
}

.warning {
  background: var(--orange);
}

.danger {
  background: var(--danger);
}

.disabled {
  background: var(--gray);
}

.base-button__text {
  color: var(--white);
  font-size: 1.2em;
}

button {
  text-shadow: none;
}
</style>
