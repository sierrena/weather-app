<template>
  <div>
    <b-field label="Name">
      <b-input v-model="name"></b-input>
    </b-field>
    <b-field label="City">
      <b-input v-model="city"></b-input>
    </b-field>
    <b-button type="is-primary">Submit </b-button>
  </div>
</template>

<script>
export default {
  methods: {
    onClick() {},
  },
  data() {
    return {
      name: "",
      city: "",
    };
  },
};
</script>

<style lang="scss" scoped></style>
