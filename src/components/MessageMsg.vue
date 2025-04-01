<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
    nome: 'MessageMsg',
    props: {
        msg: String
    }
}
</script>

<style scoped>
.message-container {
    background-color: #CCE5FF;
    border: 2px solid #B8DAFF;
    color: #004085;
    padding: 10px;
    border-radius: 5px;
    max-width: 400px;
    margin: 30px auto;
    
    
}
</style>