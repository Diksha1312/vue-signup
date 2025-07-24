<template>
  <form>
    <label>Email:</label>
    <input type="email" v-model="email" required>
  </form>
</template>

<script>
export default {
    data() {
        return {
            email: ''
        };
    },
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    padding: 40px;
    background: white;
    border-radius: 10px;
    text-align: left;
}
label {
    display: inline-block;
    font-weight: bold;  
    color: #aaa;
    margin: 25px 0 15px;
    font-size: 0.9em;
    text-transform: uppercase;
    letter-spacing: 1px;
}

input {
    display: block;
    width: 100%;
    padding: 10px 6px;
    border: none;
    border-bottom: 1px solid #ddd;
    box-sizing: border-box;
    color: #555;    
}
</style>