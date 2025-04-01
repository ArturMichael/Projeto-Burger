<template>
  <div>
      <div>
          <message-msg :msg="msg" v-show="msg"/>
      </div>
      <div>
         <form id="burguer-form" @submit="criarBurguer">
              <div class="input-container">
                  <label for="Nome">Nome do Cliente:</label>
                  <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite seu nome" required>
              </div>
              <div class="input-container">
                  <label for="pao">Escolha o pão</label>
                  <select name="pao" id="pao" v-model="pao">
                      <option value="">Selecione o seu pão</option>
                      <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
  
                  </select>
              </div>
              <div class="input-container">
                  <label for="carne">Escolha sua carne:</label>
                  <select name="carne" id="carne" v-model="carne">
                      <option value="">Selecione o tipo de carne</option>
                      <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                  </select>
              </div>
              <div id="opcionais-container" class="input-container">
                  <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                  <div class="checkbox-container" v-for="opcionais in opcionaisdata" :key="opcionais.id">
                      <input type="checkbox" name="opcionais" v-model="Opcionais" :value="opcionais.tipo"> 
                      <span>{{ opcionais.tipo }}</span>
                  </div>
              </div>
              <div class="input-container">
                  <input type="submit" class="submit-btn" value="Criar meu Burguer">
              </div>
         </form> 
      </div>
  </div>
  </template>
  
  <script>
import MessageMsg from './MessageMsg.vue';
  export default {
  components: { MessageMsg },
      nome: 'BurguerForm',
      data() {
          return {
             paes: null,
             carnes: null,
             opcionaisdata: null, 
             nome: null,
             pao: null,
             carne: null,
             opcionais: [],
             msg: null
          }
      },
      methods: {
         async getIngredientes() {
           const req = await fetch('http://localhost:3000/ingredientes');
           const data = await req.json();
  
           this.paes = data.paes;
           this.carnes = data.carnes;
           this.opcionaisdata = data.opcionais;
         },
         async criarBurguer(e) {
          e.preventDefault();
  
          const data = {
              nome: this.nome,
              pao: this.pao,
              carne: this.carne,
              opcionais: Array.from(this.opcionais),
              status: "solicitado"
          }
          const datajson = JSON.stringify(data);
          console.log(datajson);
          const req = await fetch("http://localhost:3000/burgers", {
              method: "POST",
              headers: {
                  "Content-Type": "application/json"
              },
              body: datajson
          });
          const res = await req.json();

          console.log(res);
          

          this.msg = `Seu pedido foi criado com sucesso! ID: ${res.id}`;

          setTimeout(() => {
              this.msg = "";
          }, 3000);

          this.nome = "";
          this.pao = "";
          this.carne = "";
          this.opcionais = "";
         }
      },
      mounted() {
          this.getIngredientes();
      },
  }
  </script>
  
  <style scoped>
   #burguer-form {
      max-width: 400px;
      margin: 0 auto;
   }
  
   .input-container {
      display: flex;
      flex-direction: column;
      margin-bottom: 20px;
   }
  
   label {
      font-weight: bold;
      margin-bottom: 15px;
      color: #222;
      padding: 5px 10px;
      border-left: 4px solid #FCBA03;
   }
  
   input, select {
      padding: 5px 10px;
      width: 300px;
   }
  
   #opcionais-container {
      flex-direction: row;
      flex-wrap: wrap;
   }
  
   #opicionai-title {
     width: 100%;
   }
  
   .checkbox-container {
      display: flex;
      align-items: flex-start;
      margin-bottom: 20px;
      width: 50%;
   }
  
   .checkbox-container span,
   .checkbox-container input {
          width: auto; 
  }
  
  .checkbox-container span {
      margin-left: 6px;
      font-weight: bold;
  }
  
  .submit-btn {
         background-color: #222;
          color: #FCBA03;
          border: 2px solid #222;
          padding: 10px;
          cursor: pointer;
          font-size: 16px;
          font-weight: bold; 
          transition: .5s;
  }
  
  .submit-btn:hover {
      background-color: transparent;
      color: #222
      
  }
  
  </style>
  
  