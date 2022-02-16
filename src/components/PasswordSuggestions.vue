<template>
  <div>
    <ul class="text-danger">
      <li v-for="(item, index) in suggestions" :key="index">
        {{item}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "PasswordSuggestions",
  props: ["suggestions"],
};
</script>
