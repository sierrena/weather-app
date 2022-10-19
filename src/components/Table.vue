<template>
  <div class="d-flex justify-content-center">
    <b-table
      :data="
        data?.map((dw) => {
          dw.main['dt_txt'] = dw.dt_txt;
          return dw.main;
        })
      "
      :columns="columns"
      :hoverable="true"
      :sortable="true"
      centered
    ></b-table>
  </div>
</template>

<script>
export default {
  props: {
    data: [],
  },
  methods: {},
  data() {
    return {
      columns: [
        {
          field: "dt_txt",
          label: "Date",
        },
        {
          field: "feels_like",
          label: "Feels Like",
        },
        {
          field: "grnd_level",
          label: "Ground Level",
        },
        {
          field: "humidity",
          label: "Humidity",
        },
        {
          field: "pressure",
          label: "Pressure",
        },
        {
          field: "sea_level",
          label: "Sea Level",
        },
        {
          field: "temp",
          label: "Temperature",
        },
        {
          field: "temp_kf",
          label: "Temp KF",
        },
        {
          field: "temp_max",
          label: "Temp Max",
        },
        {
          field: "temp_min",
          label: "Temp Min",
        },
      ],
    };
  },
  mounted() {
    console.log(this.data);
  },
};
</script>

<style lang="scss" scoped></style>
