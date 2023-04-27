<script setup>
// import Form  from './components/Form.vue';
import Table from './components/Table.vue';


</script>


<template>
  <div class="container-fluid">
    <div class="brand-title">Demo Test</div>
  <Table/>
</div>
</template>




<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;900&display=swap');

input {
  caret-color: red;
}

body {
  margin: auto;
  background: #ecf0f3;
  align-items: center;
  text-align: center;
  justify-content: center;
  place-items: center;
  overflow: hidden;
  font-family: poppins;
}

.container-fluid {
  width: 100%;
  text-align: center;
  box-sizing: border-box;
}


.brand-title {
  margin-top: 10px;
  margin-bottom: 10px;
  font-weight: 900;
  font-size: 1.8rem;
  color: #009879;
  letter-spacing: 1px;
}
</style>