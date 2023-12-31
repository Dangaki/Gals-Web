<script lang="ts">
import { projetoStore } from '@/stores/projetoStore'
import { computed } from 'vue'
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'AreaCodigo',
  props: {
    titulo: String
  },
  data() {
    return {
      texto: 'Area de Texto para teste'
    }
  },
  setup() {
    const store = projetoStore()

    const selecionado = computed(() => {
      return store.selecionado
    })

    const projetos = computed(() => {
      return store.listaProjetos
    })

    return {
      store,
      projetos,
      selecionado
    }
  },
  watch: {
    selecionado() {
      const definicoesRegulares = document.getElementById('textoDefinicoesRegulares')
      const tokens = document.getElementById('textoTokens')
      const naoTerminais = document.getElementById('textoNaoTerminais')
      const gramatica = document.getElementById('textoGramatica')
      const saida = document.getElementById('textoSaida')
      const simulador = document.getElementById('textoSimulador')

      if (this.selecionado == -1) return

      if (definicoesRegulares != null)
        (definicoesRegulares as HTMLInputElement).value =
          this.projetos[this.selecionado].regularDefinitions
      if (tokens != null)
        (tokens as HTMLInputElement).value = this.projetos[this.selecionado].tokens
      if (naoTerminais != null)
        (naoTerminais as HTMLInputElement).value = this.projetos[this.selecionado].nonTerminals
      if (gramatica != null)
        (gramatica as HTMLInputElement).value = this.projetos[this.selecionado].grammar
      if (saida != null)
        (saida as HTMLInputElement).value = this.projetos[this.selecionado].consoleExit
      if (simulador != null)
        (simulador as HTMLInputElement).value = this.projetos[this.selecionado].textSimulator
    }
  },
  methods: {}
})
</script>

<template>
  <div class="caixa">
    <p class="caixa__titulo">{{ titulo }}</p>

    <div v-if="projetos[selecionado] == undefined" class="caixa__interna">
      <textarea
        name="textoCodigoVazio"
        class="texto__codigo"
        :disabled="selecionado == -1"
      ></textarea>
    </div>
    <div v-else-if="titulo == 'Definições Regulares'" class="caixa__interna">
      <textarea
        id="textoDefinicoesRegulares"
        name="textoCodigo"
        rows="4"
        cols="50"
        class="texto__codigo"
        spellcheck="false"
        v-model="projetos[selecionado].regularDefinitions"
        :disabled="selecionado == -1"
      ></textarea>
    </div>
    <div v-else-if="titulo == 'Tokens'" class="caixa__interna">
      <textarea
        id="textoTokens"
        name="textoCodigo"
        rows="4"
        cols="50"
        class="texto__codigo"
        spellcheck="false"
        v-model="projetos[selecionado].tokens"
        :disabled="selecionado == -1"
      ></textarea>
    </div>
    <div v-else-if="titulo == 'Não Terminais'" class="caixa__interna">
      <textarea
        id="textoNaoTerminais"
        name="textoCodigo"
        rows="4"
        cols="50"
        class="texto__codigo"
        spellcheck="false"
        v-model="projetos[selecionado].nonTerminals"
        :disabled="selecionado == -1"
      ></textarea>
    </div>
    <div v-else-if="titulo == 'Gramática'" class="caixa__interna">
      <textarea
        id="textoGramatica"
        name="textoCodigo"
        rows="4"
        cols="50"
        class="texto__codigo"
        spellcheck="false"
        v-model="projetos[selecionado].grammar"
        :disabled="selecionado == -1"
      ></textarea>
    </div>
    <div v-else-if="titulo == 'Saida'" class="caixa__interna">
      <textarea
        id="textoSaida"
        name="textoCodigo"
        rows="4"
        cols="50"
        class="texto__codigo"
        spellcheck="false"
        disabled
        v-model="projetos[selecionado].consoleExit"
      ></textarea>
    </div>
    <div v-else-if="titulo == 'Simulação'" class="caixa__interna">
      <textarea
        id="textoSimulacao"
        name="textoCodigo"
        rows="4"
        cols="50"
        class="texto__codigo"
        spellcheck="false"
        v-model="projetos[selecionado].textSimulator"
        :disabled="selecionado == -1"
      ></textarea>
    </div>
  </div>
</template>

<style scoped>
.texto__codigo {
  outline: none;
  resize: none;
  width: 99%;
  height: calc(100% - 7px);
  -webkit-box-sizing: border-box; /* Safari/Chrome, other WebKit */
  -moz-box-sizing: border-box; /* Firefox, other Gecko */
  box-sizing: border-box; /* Opera/IE 8+ */

  font-family: 'Fira Code';

  white-space: pre;
}

.caixa {
  margin: 0px;
  padding: 0px;
  width: 100%;
  height: 100%;

  border-radius: 5px;
  background-color: white;

  flex-grow: 1;

  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.caixa__interna {
  margin: 0px;
  padding: 3px;
  width: 100%;
  height: calc(100% - 21.333px);
}

.caixa__titulo {
  font-family: 'IBM Plex Sans';
  font-weight: 600;
  color: #424242;

  border-bottom: 1px solid;
  border-color: #b1b1b1;

  text-align: center;
  margin: 0px;
  padding: 0px;
}
</style>
