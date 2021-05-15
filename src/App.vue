<template>
  <div>
    <h1>Vue conta Vogais e Consoantes</h1>
    <label>
      Digite uma palavra:
      <input autofocus type="text" @keyup.enter="newWord($event)" />
    </label>

    <p>Lista de Palavras:</p>

    <ul v-if="!!words && words.length > 0">
      <li v-for="(word, index) of words" :key="word + index" class="divWords">
        <button
          @click="removeWord(word, totalVogais[index])"
          class="waves-effect waves-light btn-small red"
        >
          x
        </button>
        &nbsp;&nbsp;&nbsp;
        <span>{{ word }}</span>
        &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;
        <span>
          <div>Total de Vogais: {{ totalVogais[index] }}</div>
          <div>Total de Consoantes: {{ totalConsoantes[index] }}</div>
          <div>Total de Letras: {{ totalVogais[index] + totalConsoantes[index] }}</div>
        </span>
      </li>
    </ul>
    <p v-else>Nenhuma palavra cadastrada.</p>
  </div>
</template>

<script>
export default {
  name: 'app',

  data() {
    return {
      words: [],
      totalVogais: [],
      totalConsoantes: [],
    };
  },

  methods: {
    newWord: function (event) {
      let totalVogal = 0;
      let vogais = ['a', 'e', 'i', 'o', 'u'];
      let i;

      const word = event.target.value.trim();

      for (i = 0; i < word.length; i++) {
        if (vogais.indexOf(word[i]) != -1) {
          totalVogal++;
        }
      }

      const totalConsoante = word.length - totalVogal;

      this.totalVogais.push(totalVogal);
      this.totalConsoantes.push(totalConsoante);

      if (!this._canAddWord(word)) return;

      this.words.push(word);
    },

    _canAddWord: function (word) {
      return !!word && this.words.filter(word => word.description === word).length === 0;
    },

    /**
     * Excluindo a palavra
     */
    removeWord(word, vogal) {
      this.words.splice(this.words.indexOf(word), 1);
      this.totalVogais.splice(this.totalVogais.indexOf(vogal), 1);
      this.totalConsoantes.splice(this.totalConsoantes.indexOf(vogal), 1);
    },
  },
};
</script>

<style>
body {
  padding: 20px;
  background: rgb(240, 243, 240);
}

.divWords {
  display: flex;
  justify-content: flex-start;
  margin-bottom: 10px;
  border: solid rgb(228, 220, 211) 1px;
}
</style>
