<script>
export default {
  props: {
    addRandomAbsence: Function,
  },
};
</script>

<template>
  <button class="absence-card" @click="addRandomAbsence"><slot /></button>
</template>



<style lang="scss" scoped>
button {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px;
    border-radius: 15px;
    background-color: rgba(16, 119, 137, 0.402);
    width: 150px;
    margin: 10px;
    font-size: 100px;
    box-shadow: 2px 6px 5px rgba(0, 0, 0, 0.2);
    cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s, background-color 0.2s;
  
    &:hover {
      transform: scale(1.00); /* "Lätt förstoring vid hover" */
      box-shadow: 3px 8px 6px rgba(0, 0, 0, 0.2);
      background-color: rgba(0, 57, 88, 0.518);
    }
  
    &:active {
      transform: scale(0.95); /* Lätt förminskning vid klick */
    }
  }
</style>
