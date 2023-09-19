<script setup>
// import TheWelcome from '../components/TheWelcome.vue'
import { ref } from 'vue'
import axios from 'axios'
import '/public/img.png'
import '/public/upload.png'

let submitButton = ref("Submit");

let fullname = ref("");
let phone = ref("");
let email = ref("");
let address = ref("");
let laptop = ref("");
let receipt = ref("");

async function submitForm() {

  try {
    submitButton.value = "Submitting... Please wait";
    const form = new FormData();

  form.append(fullname, fullname.value);
  form.append(phone, phone.value);
  form.append(email, email.value);
  form.append(address, address.value);
  form.append(laptop, laptop.value);
  form.append(receipt, receipt.value);

  const response = await axios.post("https://testbackend-ya01.onrender.com/api/v1/users/register", form, {
    headers: {
      "Content-Type": "multipart/form-data"
    }
  });

  if(response.status == 201) {
    alert("Submitted Successfully!");
  }
  } catch (error) {
    console.log(error);
    alert("An error occurred");
  } finally {
    submitButton.value = "Submit";
  }
}

function handleFile(event) {
  receipt.value = event.target.files[0];
}

</script>

<template>
  <div class="flex-it">
    <form class="form-space">
      <div class="register">Register with us</div>
      <div class="swap">Swap your old laptop for a new one</div>
      <label for="full-name">Full name</label>
      <input type="text" id="full-name" placeholder="John Doe" v-model="fullname">

      <label for="phone-number">Phone Number</label>
      <input type="text" id="phone-number" placeholder="+234000000000" v-model="phone">

      <label for="email">Email</label>
      <input type="text" id="email" placeholder="mailat@example.com" v-model="email">

      <label for="address">Address</label>
      <input type="text" id="address" placeholder="38 Crescent Avenue" v-model="address">

      <label for="laptop-specification">Laptop Specification</label>
      <select type="text" id="laptop-specification" v-model="laptop">
        <option value="" selected>Select Laptop Type</option>
        <option value="hp">HP</option>
        <option value="dell">DELL</option>
        <option value="acer">ACER</option>
        <option value="macbook">MACBOOK</option>
      </select>

      <div>Upload receipt of old laptop</div>
      <label for="old-laptop-receipt" class="receipt-label">
        <img src="/upload.png" />
        <input type="file" id="old-laptop-receipt" v-on:change="handleFile($event)"> <br />
      </label>

      <div class="submit-button-wrapper">
        <button @click.prevent="submitForm">{{ submitButton }}</button>
      </div>
    </form>
    <img src="img.png" />
  </div>
</template>

<style>
.flex-it {
  display: flex;
  width: 100%;
  justify-content: space-between;
}

.flex-it>div {
  width: 50%;
}

.flex-it>img {
  width: 50%;
}

.form-space {
  padding: 60px 94px 60px 40px;
  background-color: #F9F9F9;
}

input,
select {
  width: 100%;
  padding: 15px 20px;
  border: none;
  background-color: #FFFFFF;
  margin-top: 5px;
  margin-bottom: 20px;
  border-radius: 8px;
  box-sizing: border-box;
}

label,
.label {
  display: inline-block;
  margin-bottom: 5px;
}

.submit-button-wrapper {
  margin-top: 20px;
}

.submit-button-wrapper>button {
  background-color: #335CA6;
  color: white;
  padding: 10px 30px;
  border: none;
  border-radius: 5px;
}

.receipt-label {
  background-color: white;
  justify-content: center;
  align-items: center;
  display: flex;
  padding: 10px 25px;
  display: inline-block;
  background-size: cover;
  border-radius: 8px;
  display: inline-block;
  margin-top: 5px;
}

#old-laptop-receipt {
  display: none;
}

.receipt-label>img {
  height: 30px;
  width: 30px;
  cursor: pointer;
}

input:focus {
  outline: none;
}

* {
  font-family: 'Inter', sans-serif;
  font-weight: 500;
}

.register {
  font-weight: 600;
  font-size: 32px;
}

.swap {
  font-weight: 300;
  margin-bottom: 20px;
}

@media screen and (min-width: 425px) and (max-width: 768px) {
  .form-space {
    padding: 40px 54px 40px 20px;
  }
}

@media screen and (max-width: 425px) {
  .form-space {
    padding: 40px 25px;
  }

  .flex-it>img {
    display: none;
  }
}
</style>