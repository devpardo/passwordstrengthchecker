<template>
  <b-card class="mt-5">
    <h1 class="m-0 mb-5 text-center">Is your password strong enough?</h1>
    <b-input-group class="mb-4">
      <b-form-input
        name="dmpassword"
        v-model="passwordInput"
        :type="passwordFieldType"
        size="lg"
        placeholder="Type a password"
        @keyup.enter="checkStrength()"
      ></b-form-input>

      <b-input-group-append>
        <b-button @click="showPassword" size="sm" text="Button">
          <b-icon icon="eye"></b-icon>
        </b-button>
      </b-input-group-append>
    </b-input-group>

    <PasswordStrength :strength="passwordStrength"/>
    <PasswordSuggestions :suggestions="passwordSuggestions"/>
  </b-card>
</template>

<script>
import PasswordStrength from '@/components/PasswordStrength'
import PasswordSuggestions from '@/components/PasswordSuggestions'
export default {
  name: "PasswordInput",
  components: {
    PasswordStrength,
    PasswordSuggestions
  },
  data() {
    return {
      passwordInput: '',
      passwordFieldType: 'password',
      passwordStrength: 0,
      passwordSuggestions: []
    };
  },
  methods: {
    showPassword() {
      this.passwordFieldType = this.passwordFieldType === 'password' ? 'text' : 'password';
    },
    checkStrength() {
      this.$http.post('https://o9etf82346.execute-api.us-east-1.amazonaws.com/staging/password/strength', {
        'password': this.passwordInput
      }).then((res) => {
        console.log(res.data);

        let result = res.data;
        this.passwordStrength = result.score;
        this.passwordSuggestions = result.suggestions;
      });
    }
  }
};
</script>
