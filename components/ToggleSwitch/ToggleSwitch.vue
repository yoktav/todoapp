<template>
  <button
    type="button"
    :class="['c-toggle-switch', { 'is-active': isActive }]"
    @click="toggleSwitch"
  >
    <span v-if="hasText" class="c-toggle-switch__text c-toggle-switch__text--primary">
      {{ primaryText }}
    </span>
    <span v-if="hasText" class="c-toggle-switch__text c-toggle-switch__text--secondary">
      {{ secondaryText }}
    </span>
  </button>
</template>

<script>
export default {
  props: {
    hasText: {
      type: Boolean,
      default: true,
      required: true,
    },
    primaryText: {
      type: String,
      default: 'ON',
    },
    secondaryText: {
      type: String,
      default: 'OFF',
    },
    isActive: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      ACTIVE_CLASS: 'is-active',
    };
  },
  methods: {
    toggleSwitch() {
      this.$el.classList.toggle(this.ACTIVE_CLASS);
      this.$emit('clicked');
    },
  },
};
</script>

<style lang="scss" scoped>
@import './ToggleSwitch';
</style>
