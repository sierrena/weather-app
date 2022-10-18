<template>
  <div>
    <b-table :data="props.main"></b-table>
  </div>
</template>

<script>
export default {
  props: {
    weatherData: [],
  },
  methods: {},
  data() {
    return {
      props: Array,
    };
  },
  mounted() {
    console.log(this.props);
  },
};
</script>

<style lang="scss" scoped></style>
