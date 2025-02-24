<script setup lang="ts">
import Modal from './components/Modal.vue'
import LoremIpsum from './components/LoremIpsum.vue'
import { ref } from 'vue'

const open = ref(false)
const open2 = ref(false)

const toggleModal = () => {
  open.value = !open.value
}
const toggleModal2 = () => {
  open2.value = !open2.value
}
</script>

<template>
  <main class="main-container">
    <div class="teleport-description">
      <h2><strong>O que é o <code>&lt;Teleport/&gt;</code> e por que é importante?</strong></h2>
      <br />
      <p>
        O <code>&lt;Teleport/&gt;</code> no Vue é um recurso que permite "teletransportar" um elemento do DOM para outro
        local na árvore de componentes sem mudar a sua posição no código.
        Ele é útil quando você precisa renderizar elementos fora do contexto do componente atual, como modais, tooltips
        ou popups, que precisam ser renderizados fora da hierarquia de layout para evitar problemas de overflow e de
        posicionamento.
      </p>
      <br />
      <p>
        Usar o <code>&lt;Teleport/&gt;</code> para modais, por exemplo, evita que eles fiquem limitados pelo
        <code>overflow</code> ou pelo contexto de estilo do componente que os contém.
      </p>
      <br />
      <p> Além disso, permite garantir que o modal seja colocado em um local onde a sobreposição de fundo e o
        comportamento visual sejam mais apropriados para a interface do usuário.</p>
    </div>

    <button @click="toggleModal" class="open-modal-button">Ativar Teleport !</button>
    

    <img class="image-teleport" src="./assets/teleport-dom.png" alt="Representações do comportamento do Teleport no vue" />


    <Modal :height="'auto'" :width="'450px'" v-model="open">
      <LoremIpsum class="lorem-content" />
      <div class="bottom-modal ">
        <button @click="open = false">Fechar</button>
        <button @click="toggleModal2" class="open-modal-button">Ativar Teleport 2 !</button>
      </div>
    </Modal>
    <Modal title="Título do Modal 2" :height="'auto'" :width="'600px'" v-model="open2">
      <LoremIpsum />
      <br />
      <LoremIpsum />
      <br />
      <LoremIpsum />
    </Modal>
  </main>
</template>

<style scoped>

.image-teleport{
  height: 76dvh;
  width: 70dvw;
}

.lorem-content {
  margin: 24px 10px;
}

.bottom-modal {
  display: flex;
  justify-content: space-between;
  align-items: start;
  gap: 10px;

  button {
    flex: 1;
  }
}

.main-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 20px;
}

.teleport-description {
  margin-bottom: 20px;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 600px;
  font-size: 14px;
}

.open-modal-button {
  padding: 0.6em 1.2em;
  background-color: #4CAF50;
  color: white;
  border: 1px solid transparent;
  border-radius: 8px;
  font-size: 12px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.open-modal-button:hover {
  background-color: #45a049;
  border-color: #64ff86;
}

pre {
  padding: 10px;
  border-radius: 5px;
  font-size: 13px;
}
</style>
