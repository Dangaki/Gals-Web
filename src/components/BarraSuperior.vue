<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'BarraSuperior',
  components: {}
})
</script>

<template>
  <div class="barra__superior">
    <span class="logo">GALS</span>

    <button class="botao__gerar__codigo">Gerar Código</button>

    <span> </span>
  </div>
</template>

<style scoped>
.logo {
  font-family: 'Lexend';
  font-weight: 700;
  font-size: 26px;
  line-height: 45px;
  display: flex;
  align-items: center;
  text-align: center;

  color: #424242;
}

.logo::before {
  content: '\00a0\00a0';
  color: #9ed15c;
}

.logo::after {
  content: '\00a0WEB';
  color: #9ed15c;
}

.botao__gerar__codigo {
  font-family: 'IBM Plex Sans';
  font-weight: bold;
  font-size: 15px;
  color: white;
  text-decoration: none;

  text-align: center;
  vertical-align: middle;

  border: none;
  border-radius: 12px;
  background-color: #9ed15c;

  width: 150px;
  height: 38px;
  margin: 0;

  display: flex;
  align-items: center;
  justify-content: center;
}

.botao__gerar__codigo::before {
  content: url(@/assets/icons/Gerar_Codigo.svg);
  vertical-align: middle;
}

.botao__gerar__codigo:hover {
  background-color: #749a43;
}

.botao__gerar__codigo:active {
  background-color: #749a43;
  box-shadow: 0 1px #666;
  transform: translateY(1px);
}

.barra__superior {
  background-color: white;
  width: 100wh;
  height: 50px;
  display: flex;
  flex-shrink: 0;
  margin: 0px;
  padding: 0px;

  justify-content: space-between;
  align-items: center;
}
</style>
