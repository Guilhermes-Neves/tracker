<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro' : modoEscuro}">
    <div class="column is-one-quarter">
      <BarraLateral @aoAlterarModo="alterarModo"/>
    </div>
    <div class="column is-three-quarters conteudo">
      <Formulario @aoSalvarTarefa="salvarTarefa"/>
      <div class="lista">
        <Box v-if="semTarefas">
          Você não está muito produtivo hoje <span class="has-text-weight-bold">:(</span>
        </Box>
        <Tarefa v-for="(tarefa, index) in tarefas" :tarefa="tarefa" :key="index"/>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Formulario from "./components/Formulario.vue";
import BarraLateral from "./components/BarraLateral.vue";
import Tarefa from "./components/Tarefa.vue";
import Box from "./components/Box.vue";
import ITarefa from "./interfaces/ITarefa"

export default defineComponent({
  name: "App",
  components: {
    Formulario,
    BarraLateral,
    Tarefa,
    Box
  },
  data () {
    return {
      tarefas: [] as ITarefa[],
      modoEscuro: false
    }
  },
  methods: {
    salvarTarefa (tarefa:ITarefa) : void {
      this.tarefas.push(tarefa)
    },
    alterarModo (modoEscuro: boolean) : void {
      this.modoEscuro = modoEscuro
    }
  },
  computed: {
    semTarefas () :boolean {
      return this.tarefas.length == 0
    }
  }
});
</script>

<style>
main {
  --bg-primario: #fff;
  --texto-primario: #000;
}
main.modo-escuro {
  --bg-primario: #2b2d42;
  --texto-primario: #ddd;
}
.lista {
  padding: 1.25rem;
}
.conteudo {
  background-color: var(--bg-primario);
}
h1 {
  color: #fff;
  font-size: 2em;
}
</style>