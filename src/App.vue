<template>
  <div>
    <h1>Vue conta Vogais e Consoantes</h1>
    <label>
      Digite uma palavra:
      <input autofocus type="text" @keyup.enter="newWord($event)" />
    </label>

    <p>Lista de Palavras:</p>

    <ul v-if="!!words && words.length > 0">
      <li v-for="(word, index) of words" :key="word + index">
        <button @click="removeWord(word)" class="waves-effect waves-light btn-small red">x</button>
        &nbsp;&nbsp;&nbsp;
        <span> {{ word }} </span>
        &nbsp;&nbsp;&nbsp;
        <span>Total de Vogais: {{ totalVogais[index] }}</span>
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
          // console.log(totalVogal);
        }
      }

      this.totalVogais.push(totalVogal);

      /**
       * Verificamos se realmente podemos incluir a
       * nova tarefa
       */
      if (!this._canAddWord(word)) return;

      this.words.push(word);
    },

    /**
     * Verifica a possibilidade da inclusão da palavra
     * com base nas seguintes regras:
     *
     * 1) Palavra existente
     * 2) Descrição ainda não existe na listagem de palavras
     */
    _canAddWord: function (word) {
      return !!word && this.words.filter(word => word.description === word).length === 0;
    },

    /**
     * Excluindo a palavra
     */
    removeWord(word) {
      this.words.splice(this.words.indexOf(word), 1);
    },
  },
};
</script>

<style>
body {
  padding: 20px;
}

.completed {
  color: green;
  font-weight: bold;
}
</style>
