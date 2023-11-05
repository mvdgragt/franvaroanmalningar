<script>
export default {
  props: {
    absence: Object,
    getReason: Function,
    formatDateTime: Function,
  },
};
</script>

<template>
  <div class="absence-card-container">
    <div class="absence-card">
      <p class="name">{{ absence.firstName }} {{ absence.lastName }}</p>
      <p>
        {{ formatDateTime(absence.dateTimeFrom) }} -
        {{ formatDateTime(absence.dateTimeTo) }}
      </p>
      <p>{{ getReason(absence.reasonGuid) }}</p>
    </div>
  </div>
</template>


<style lang="scss" scoped>
.absence-card-container {
  flex-wrap: wrap;
  justify-content: space-between;
}
.absence-card {
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f7f7f7;
  font-size: small;
  font-family: Arial, Helvetica, sans-serif;
  min-height: 120px;
  box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}
.name {
  font-weight: bold;
  font-size: 1.3em;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
