<template>
  <div>
    <h2>Faça seu pedido</h2>
    <form @submit.prevent="enviarPedido">
      <div>
        <label for="nome">Nome:</label>
        <input type="text" v-model="pedido.nome" required />
      </div>

      <div>
        <label for="numero">Número:</label>
        <input type="text" v-model="pedido.numero" required />
      </div>

      <div>
        <label for="endereco">Endereço:</label>
        <input type="text" v-model="pedido.endereco" required />
      </div>

      <div>
        <label for="itens">Itens:</label>
        <textarea v-model="pedido.itens" required></textarea>
      </div>

      <div>
        <label for="total">Total:</label>
        <input type="number" v-model="pedido.total" required />
      </div>

      <button type="submit">Enviar Pedido</button>
    </form>

    <p v-if="responseMessage">{{ responseMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      pedido: {
        nome: '',
        numero: '',
        endereco: '',
        itens: '',
        total: '',
      },
      responseMessage: '',
    }
  },
  methods: {
    enviarPedido() {
      // Transformando a lista de itens em um array
      this.pedido.itens = this.pedido.itens.split(',').map((item) => item.trim())

      // Enviar dados para o backend
      axios
        .post('http://localhost:3000/pedidos', this.pedido)
        .then((response) => {
          this.responseMessage = response.data.message
        })
        .catch((error) => {
          console.error('Erro ao enviar pedido:', error)
          this.responseMessage = 'Erro ao enviar pedido.'
        })
    },
  },
}
</script>

<style scoped>
/* Adicione seu estilo aqui */
</style>
