<template>
    <div class="container">
      <div class="row text-center">
        <div class="col-md-4"></div>
        <div class="col-md-4">
          <table width="100%">
            <tr>
              <td width="80%">
                <h4 style="font-size: 2em;">PELADA ORGANIZADA</h4>
              </td>
              <td width="20%">
                <img width="100px" height="100px" src="https://cdn-icons-png.flaticon.com/512/53/53283.png"/>
              </td>
            </tr>
          </table>
        </div>
        <div class="col-md-4"></div>
      </div>
      <div class="row">
        <div class="col-md-12">
          <h6>Escolha sua pelada:</h6>
        </div>
        <div class="col-md-12">
          <table class="table">
            <thead>
              <th>#</th>
              <th>Nome</th>
              <th>Data</th>
              <th>Hora</th>
              <th>Localização</th>
              <th></th>
            </thead>
            <tbody v-for="(pelada, i) in data">
              <tr >
                <td>1</td>
                <td>
                  <div class="row">
                    <div class="col-md-12">
                      <label>{{ pelada.nome }}</label>
                    </div>
                  </div>
                </td>
                <td>
                  <label>{{ pelada.data }}</label>
                </td>
                <td>
                  <label>{{ pelada.horaInicio }} - {{ pelada.horaFim }}</label>
                </td>
                <td>
                  <label>Campo de Ronaldo - Arez/RN</label>
                </td>
                <td>
                  <button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#modalSenha">ENTRAR</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
       <!-- Modal -->
       <div class="modal fade" id="modalSenha" tabindex="-1" aria-hidden="true">
          <div class="modal-dialog">
              <div class="modal-content">
              <div class="modal-header">
                  <h1 class="modal-title fs-5" id="exampleModalLabel">Entrar na pelada</h1>
                  <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
              </div>
              <div class="modal-body">
                  <label>É necessário uma senha para entrar nessa pelada, digite a senha no campo abaixo:</label><br>
                  <input class="form-control" type="password"/>
              </div>
              <div class="modal-footer">
                  <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
                  <button type="button" class="btn btn-primary">Entrar</button>
              </div>
              </div>
          </div>
      </div>
    </div>
  </template>
  <script setup>
    const { data } = await useFetch('http://localhost:3333');

  </script>