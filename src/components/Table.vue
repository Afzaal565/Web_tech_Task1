<script setup>
import { ref } from 'vue';
import axios from 'axios';

const deviceUserName = ref('');
const webUserName = ref('');

const timesheetData = ref([]);

const submitForm = async () => {
  const data = {
    deviceUserName: deviceUserName.value,
    webUserName: webUserName.value,
  };

  try {
    const response = await axios.post('https://frontier.earnflex.com/get_all_timesheet_data', data);
    console.log(response.data.data);
    timesheetData.value = response.data.data;
    deviceUserName.value = '';
    webUserName.value = '';
  } catch (error) {
    console.log(error);
  }
};

</script>

<template>
    <div>
        <form class="new-form" @submit.prevent="submitForm" >
            <div class="form-div">
                <label>Device User Name</label>
                <input type="text" v-model="deviceUserName" placeholder="Device User Name">
            </div>
            <div class="form-div">
                <label>Web User Name</label>
                <input type="text" v-model="webUserName" placeholder="Web User Name">
            </div>
        
            <button type="submit">Display Time Sheet</button>
        </form>
        <table class="styled-table">
            <thead>
                <tr>
                    <td>Time</td>
                    <td>Book On Image</td>
                    <td>Time In</td>
                    <td>Book On Location</td>
                    <td>Book Off Image</td>
                    <td>Time Out</td>
                    <td>Book Off Location</td>
                    <td>Total Hours</td>
                </tr>
            </thead>
            
            <tbody>
                <tr v-for="entry in timesheetData" :key="entry.id">
                    <td>{{ entry.timeIn }}</td>
                    <td> <a :href="entry.bookOnImageURL" target="_blank">
                            <img :src="entry.bookOnImageURL" alt="">
                        </a>
                    </td>
                    <td>{{ entry.timeIn }}</td>
                    <td>{{ entry.bookOnLocationName }}</td>
                    <td> 
                        <a :href="entry.bookOnImageURL" target="_blank">
                            <img :src="entry.bookOffImageURL" alt="">
                        </a>
                    </td>
                    <td>{{ entry.timeOut }}</td>
                    <td>{{ entry.bookOffLocationName }}</td>
                    <td>{{ entry.hoursWorked }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>



<style scoped>
.new-form {
    display: flex;
    text-align: left;
    position: relative;
    border-radius: 12px 12px 0 0;
    padding: 15px;
    box-sizing: border-box;
    background: #ecf0f3;
    box-shadow: 14px 14px 20px #cbced1, -14px -14px 20px white;
}
.form-div {
    display: flex;
    flex-direction: column;
    margin-right: 30px;
}

label, input, button {
  display: block;
  width: 100%;
  padding: 0;
  border: none;
  outline: none;
  box-sizing: border-box;
}

label {
  margin-bottom: 4px;
}

label:nth-of-type(2) {
  margin-top: 12px;
}

input::placeholder {
  color: gray;
}

input {
    width: 300px;
    background: #ecf0f3;
    padding: 10px;
    padding-left: 20px;
    height: 50px;
    font-size: 14px;
    border-radius: 50px;
    box-shadow: inset 6px 6px 6px #cbced1, inset -6px -6px 6px white;
}

button {
  color: white;
  margin-top: 25px;
  background: #009879;
  height: 50px;
  max-width: 200px ;
  border-radius: 50px;
  cursor: pointer;
  font-weight: 900;
  box-shadow: 6px 6px 6px #cbced1, -6px -6px 6px white;
  transition: 0.5s;
}

button:hover {
  box-shadow: none;
  height: 45px;
  margin-top: 27px;
}


.styled-table {
    border-collapse: collapse;
    font-size: 0.9em;
    font-family: sans-serif;
    min-width: 400px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}

.styled-table thead tr {
    background-color: #009879;
    color: #ffffff;
    text-align: left;
}


.styled-table th,
.styled-table td {
    padding: 12px 15px;
    min-width: 140px;
}

.styled-table tbody tr {
    border-bottom: 1px solid #dddddd;
}

.styled-table tbody tr  td img {
    max-width: 100px;
    border-radius: 100px;
}

.styled-table tbody tr:nth-of-type(even) {
    background-color: #f3f3f3;
}

.styled-table tbody tr:last-of-type {
    border-bottom: 2px solid #009879;
}

.styled-table tbody tr.active-row {
    font-weight: bold;
    color: #009879;
}
</style>