<script>
  export default {
    props: {
      changeAmount: {
        type: Function,
        required: true
      },
      convert: {
        type: Function,
        required: true
      },
      error: {
        type: String,
        required: true
      }
    }
  }
</script>

<template>
  <input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Enter a number" ><br>
  <button @click="convert()">Convert</button>
  <p v-if="error != ''">{{ error }}</p>
</template>

<style scoped>
p{
  color: #FF0000;
}
input {
  margin-top: 10px;
  width: 500px;
  border-radius: 10px;
  border: 0;
  padding: 10px 15px;
  color: #5d5d5d;
  outline: none;
  font-size: 1.2em;
}

button {
  margin-top: 30px;
  padding: 15px 20px;
  color: #FFFFFF;
  text-shadow: 0 0 5px #FFFFFF;
  background: #1A032D;
  border: 0;
  text-transform: uppercase;
  cursor: pointer;
  border-radius: 3px;
  transition: 0.5s ease;
}
button:hover {
  background: #24043e;
  transform: scale(1.05);
}
</style>