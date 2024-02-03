<template>
    <div class="container">
        <div class="row mt-5">
            <div class="col-md-6">
                <nav aria-label="breadcrumb">
                    <ol class="breadcrumb">
                        <li class="breadcrumb-item" aria-current="page">
                            <a href="/">
                                Home
                            </a>
                        </li>
                        <li class="breadcrumb-item active" aria-current="page">Ver pelada</li>
                    </ol>
                </nav>
            </div>
        </div>
        <div class="row">
            <div class="col-md-6">
                <h1>Pelada da segunda</h1>
            </div>
            <div class="col-md-6">
                <!-- Button trigger modal -->
                <button class="btn btn-primary">ENTRAR</button>

               
            </div>
        </div>
        <div class="row">
            <div class="col-md-6">
                <label>Próxima pelada:</label><br>
                <table class="table" width="100%">
                    <thead>
                        <th>Data</th>
                        <th>Local</th>
                    </thead>
                    <tr>
                        <td>
                            <label>01/02/2024</label>
                        </td>
                        <td>
                            <label>Campo de Ronaldo - Arez/RN</label>
                        </td>
                    </tr>
                </table>
            </div>
        </div>
        <div class="row">
            <div class="col-md-6">
                <label><b>Histórico de peladas:</b></label><br>
                <table class="table">
                    <tr>
                        <td>
                            Data
                        </td>
                    </tr>
                </table>
            </div>
        </div>
    </div>
</template>
<script setup lang="ts">
    const peladas = await useFetch('http://localhost:3333');
    console.log(peladas);
</script>