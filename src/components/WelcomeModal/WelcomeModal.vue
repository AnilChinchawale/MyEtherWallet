<template>
  <div></div>
</template>
<script>
export default {
  props: {
    firstTimeRu: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    closeModal() {
      this.$refs.welcome.hide();
    }
  }
};
</script>

<style lang="scss" scoped>
@import 'WelcomeModal.scss';
</style>
