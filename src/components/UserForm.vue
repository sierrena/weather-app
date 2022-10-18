<template>
  <div>
    <b-field label="Name">
      <b-input v-model="name"></b-input>
    </b-field>
    <b-field label="City">
      <b-input v-model="city"></b-input>
    </b-field>
    <b-button type="is-primary" @click="onClick()">Submit </b-button>
  </div>
</template>

<script>
export default {
  methods: {
    onClick() {
      this.$emit("submitted", { name: `${this.name}`, city: `${this.city}` });
    },
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
