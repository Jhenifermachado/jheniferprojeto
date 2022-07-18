<script>
import axios from "axios";
export default {
  data() {
    return {
      jogadores: [],
      jogador: {},
      times: [],
    };
  },
  async created() {
    await this.buscarTodosOsJogadores();
    const times = await axios.get("http://localhost:4000/times");
    this.times = times.data;
  },
  methods: {
    async buscarTodosOsJogadores() {
      const jogadores = await axios.get("//localhost:4000/jogadores");
      this.jogadores = jogadores.data;
    },
    async salvar() {
      await axios.post("http://localhost:4000/jogadores", this.jogador);
      await this.buscarTodosOsJogadores();
    },
    async excluir(jogador) {
      await axios.delete(`http://localhost:4000/jogadores/${jogador.id}`);
      const indice = this.jogadores.indexOf(jogador);
      this.jogadores.splice(indice, 1);
    },
  },
};
</script>

<template>
  <main>
    <div class="container">
      <div class="title">
        <h2>Gerenciamento de times</h2>
      </div>
      <div class="form-input">
        <input type="text" placeholder="jogador" v-model="jogador.nome" />
        <input
          type="text"
          placeholder="ano de nascimento"
          v-model="jogador.anoNascimento"
        />
        <input
          type="text"
          placeholder="posição"
          v-model="jogador.posicaoJogo"
        />
        <select v-model="jogador.timeId">
          <option v-for="time in times" :key="time.id" :value="time.id">
            {{ time.nome }}
          </option>
        </select>
        <button @click="salvar">Salvar</button>
      </div>
      <div class="list-times">
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>Nome</th>
              <th>Ano Nascimento</th>
              <th>Posição de jogador</th>
              <th>Time</th>
              <th>Ações</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="jogador in jogadores" :key="jogador.id">
              <td>{{ jogador.id }}</td>
              <td>{{ jogador.nome }}</td>
              <td>{{ jogador.anoNascimento }}</td>
              <td>{{ jogador.posicaoJogo }}</td>
              <td>{{ jogador.timeId }}</td>
              <td>
                <button>Editar</button>
                <button @click="excluir(jogador)">Excluir</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </main>
</template>
<style>
.title {
  text-align: center;
  margin: 2rem 0;
}

.form-input {
  display: flex;
  justify-content: center;
  margin: 2rem 0;
}

.form-input input {
  width: 50%;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 10px;
}

.form-input button {
  padding: 0.5rem;
  border: 1px solid black;
  border-radius: 10px;
  background-color: rgb(6, 103, 40);
  color: #fff;
  font-weight: bold;
  margin-left: 1%;
}

.list-times {
  display: flex;
  justify-content: center;
}

table {
  width: 50%;
  border-collapse: collapse;
  margin: 0 auto;
  border: 1px solid black;
  font-size: 1 1rem;
  text-align: center;
}

table thead {
  background-color: rgb(255, 105, 180);
  color: whitesmoke;
  font-size: bold;
}
table thead th {
  background-color: rgb(255, 105, 180);
  color: whitesmoke;
}

table tbody tr:nth-child(odd) {
  background-color: violet;
}
</style>
