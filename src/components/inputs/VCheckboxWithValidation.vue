<template>
    <ValidationProvider :name="$attrs.label" :rules="rules" v-slot="{ errors, valid }">
        <v-checkbox
        v-bind="$attrs" 
        v-on="$listeners"
        v-model="innerValue"
        :error-messages="errors"
        value="1"
        type="checkbox"
        required
        :success="valid"
        ></v-checkbox>
    </ValidationProvider>
</template>

<script>
import { ValidationProvider } from "vee-validate";

export default {
  components: {
    ValidationProvider
  },
  props: {
    rules: {
      type: [Object, String],
      default: ""
    },
    value: {
      type: null
    }
  },
  data: () => ({
    innerValue: ""
  }),
  watch: {
    // Handles internal model changes.
    innerValue(newVal) {
      this.$emit("input", newVal);
    },
    // Handles external model changes.
    value(newVal) {
      this.innerValue = newVal;
    }
  },
  created() {
    if (this.value) {
      this.innerValue = this.value;
    }
  }
};
</script>