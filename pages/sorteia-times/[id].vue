<template>
    <div class="container">
        <div class="row mt-3">
            <div class="col-md-12">
                <button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#modalAdicionarJogadores">ADICIONAR JOGADORES</button>
            </div>
        </div>
        <div class="row mt-2">
            <div class="col-md-12">
                <h6>Lista de jogadores:</h6>
            </div>
            <div class="col-md-12">
                <table class="table">
                    <thead>
                        <th>#</th>
                        <th>Nome</th>
                        <th>Posição</th>
                        <th>Estrelas</th>
                    </thead>
                    <tbody>
                        <tr v-for="(jogador, i) in jogadores" :key="jogador">
                            <td>
                                {{ i + 1 }} -
                            </td>
                            <td>
                                {{ jogador.nome }}
                            </td>
                            <td>
                                {{ jogador.posicao }}
                            </td>
                            <td>
                                <select v-model="jogador.estrelas">
                                    <option>0.5</option>
                                    <option>1</option>
                                    <option>1.5</option>
                                    <option>2</option>
                                    <option>2.5</option>
                                    <option>3</option>
                                    <option>3.5</option>
                                    <option>4</option>
                                    <option>4.5</option>
                                    <option>5</option>
                                </select>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <button class="btn btn-primary" @click="sortear()">SORTEAR TIMES</button>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12 listaJogadores">
                
            </div>
        </div>
        <!-- Modal -->
        <div class="modal bg-light fade" id="modalAdicionarJogadores" tabindex="-1" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">Adicionar jogadores</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="row">
                        <div class="col-md-12">
                            <table class="switch">
                                <tbody>
                                    <tr>
                                        <td :class="(addByJogador) ? 'bg-primary' : 'bg-secondary'" @click="switchOption(1)">
                                            <label class="text-light">
                                                Adicionar jogador por vez
                                            </label>
                                        </td>
                                        <td :class="(addByList) ? 'bg-primary' : 'bg-secondary'" @click="switchOption(2)">
                                            <label class="text-light">
                                                Adicionar lista de jogadores
                                            </label>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <div class="row">
                        <div class="col-md-12" :style="(addByJogador) ? 'display:block;' : 'display:none;' ">
                            <fieldset class="input-group p-3">
                                <legend>Informe o nome do jogador:</legend>
                                <input class="form-control" type="text" id="nomeJogador">
                            </fieldset>
                            <fieldset class="input-group p-3">
                                <legend>Informe a posição do jogador:</legend>
                                <input class="form-control" type="text" id="posicaoJogador">
                            </fieldset>
                            <fieldset class="input-group p-3">
                                <legend>Informe as estrelas do jogador:</legend>
                                <select class="form-select" id="estrelasJogador">
                                    <option>0.5</option>
                                    <option>1</option>
                                    <option>1.5</option>
                                    <option>2</option>
                                    <option>2.5</option>
                                    <option>3</option>
                                    <option>3.5</option>
                                    <option>4</option>
                                    <option>4.5</option>
                                    <option>5</option>
                                </select>
                            </fieldset>
                        </div>
                        <div class="col-md-12" :style="(addByList) ? 'display:block;' : 'display:none;'">
                            <textarea id="inputListaJogadores"></textarea>
                        </div>
                    </div>    
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                        <button type="button" class="btn btn-primary" @click="addJogador">ADICIONAR</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
    .switch {
        width: 100%;
        text-align: center;
    }
    .switch td {
        transition: .1s linear;
        padding: 10px;
        cursor: pointer;
    }
</style>
<script setup>
    import { ref, watch } from 'vue';
    var jogadores = ref([])

    var addByJogador = ref(true);
    var addByList = ref(false);

    async function addJogador(){
        if (addByJogador.value) {
            
        } else {
            var lista = document.getElementById("inputListaJogadores").value.trim().toUpperCase()
            lista = lista.split('\n');
            lista.forEach((element) => {
                jogadores.value.push({
                    nome: element.replace("✅", ""),
                    posicao: "",
                    estrelas: 1
                });
            })
        }
    }

    function switchOption(option){
        if (option==1) {
            addByJogador.value = true;
            addByList.value = false;
        } else {
            addByList.value = true;
            addByJogador.value = false;
        }
    }
    const numeroDeTimes = 4;

    function sortear(){
        const times = Array.from({ length: numeroDeTimes }, () => []);
        var jogadoresOrdenados = ordenarPorNivel(jogadores.value);
        // Distribuir jogadores nos times de forma equilibrada
        jogadoresOrdenados.forEach((jogador, index) => {
            // Encontrar o time com o menor número de jogadores
            const timeIndex = times.reduce((minIndex, currentTime, currentIndex) =>
                currentTime.length < times[minIndex].length ? currentIndex : minIndex,
                0
            );

            // Adicionar jogador ao time
            times[timeIndex].push(jogador);
        });

        // Ajustar para garantir que cada time tenha o mesmo número de jogadores
        const numeroDeJogadoresPorTime = Math.floor(jogadores.length / numeroDeTimes);

        times.forEach((time, index) => {
            while (time.length < numeroDeJogadoresPorTime) {
                const jogador = jogadoresOrdenados.shift();
                time.push(jogador);
            }
        });

        // Exibir os times
        times.forEach((time, index) => {
            console.log(`Time ${index + 1}:`);
            time.forEach(jogador => {
                console.log(`  ${jogador.nome} (Nível ${jogador.estrelas})`);
            });
        });
    }

    // Função para ordenar os jogadores por nível
    function ordenarPorNivel(jogadores) {
        return jogadores.sort((a, b) => b.estrelas - a.estrelas);
    }


    
    
</script>