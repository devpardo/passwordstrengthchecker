<template>
  <b-progress class="mb-5" :value="strength" :max="4" animated></b-progress>
</template>

<script>
export default {
  name: 'PasswordStrength',
  props: {
    strength : {
      default: 0
    }
  }
}
</script>