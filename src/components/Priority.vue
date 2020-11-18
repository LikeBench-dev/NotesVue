<template>

  <div class="priority-container">
    <p>Priority</p>
    <div class="radio" id="newCheck">
      <input type="radio" id="light" value="light"
             v-model="note.priority">
      <label for="light" >Light</label>
    
      <input type="radio" id="middle"
             value="middle"
             v-model="note.priority">
      <label for="middle">Middle</label>
  
      <input type="radio" id="high" value="high"
             v-model="note.priority">
      <label for="high">High</label>
  
    </div>
  </div>




</template>

<script>
export default {
    props: {
        note: {
            type: Object,
            required: true
        }
    }
}

</script>

<style lang="scss" scoped>
.priority-container {
  margin: 10px 0 35px;
  .radio {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 35px 0;

    input {
      width: 30px;
      margin: 5px;
      cursor: pointer;
      &:checked +label {
        box-shadow: 0 10px 20px rgba(0, 0 , 0, .05);
        border-radius: 0 0 5px 5px;
        font-weight: 500;
      }
      &:checked +label:nth-of-type(1) {
        box-shadow: 0 10px 20px rgba(0, 0 , 0, .05);
        border-bottom: 5px solid var(--white);
      }
      &:checked +label:nth-of-type(2) {
        border-bottom: 5px solid var(--success-color);
      }
      &:checked +label:nth-of-type(3) {
        /*border-bottom: 2px solid rgba(208, 59, 59, .7);*/
        border-bottom: 5px solid var(--danger-color);
      }
    }
    label {
      margin: 5px 20px 5px 5px;
      cursor: pointer;
      &:last-child {
        margin-right: 0;
      }
    }
  }
}



</style>
