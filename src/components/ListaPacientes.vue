<!-- ESTRUTURA -->

<template>
  <div id="app" class="container">
    <div class="table-wrapper">
      <div class="table-title">
        <div class="row">
          <div class="cos-sm-6">
            <h2>
              Infectados
              <b>Sejam Bem-vindos!</b>
            </h2>
          </div>
        </div>
      </div>
      <table class="table table-striped table-hover">
        <thead>
          <tr>
            <th>ID</th>
            <th>Nome</th>
            <th>Estado</th>
            <th>Cidade</th>
            <th>Endereço</th>
            <th>Telefone</th>
            <th>Altura</th>
            <th>Peso</th>
            <th>Problema de Saúde</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody
          :class="{ active: index == currentIndex }"
          v-for="(paciente, index) in pacientes"
          :key="index"
        >
          <tr>
            <td>{{ paciente.id }}</td>
            <td>{{ paciente.nome }}</td>
            <td>{{ paciente.estado }}</td>
            <td>{{ paciente.cidade }}</td>
            <td>{{ paciente.endereco }}</td>
            <td>{{ paciente.telefone }}</td>
            <td>{{ paciente.altura }}</td>
            <td>{{ paciente.peso }}</td>
            <td>{{ paciente.prob_saude }}</td>
            <td>
              <a :href="'pacientes/' + paciente.id" class="edit" data-toggle="modal">
                <i class="material-icons" data-toggle="tooltip" title="Edit">&#xE254;</i>
              </a>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="row">
        <div class="col-sm-6">
          <a href="/adicionar" class="btn addButton" data-toggle="modal">
            Adicionar paciente
            <i class="material-icons">&#xE147;</i>
          </a>
        </div>
      </div>
    </div>
  </div>  
</template>

<!-- COMPORTAMENTO -->

<script>
import PacienteWS from "../services/PacientesWS";

export default {
  name: "listarPacientes",
  data() {
    return {
      pacientes: [],
      currentIndex: -1,
      currentPaciente: null,
      nome: ""
    };
  },
  methods: {
    obterPacientes() {
      PacienteWS.getAll()
        .then(pacientes => {
          this.pacientes = pacientes.data;
          console.log(this.pacientes);
        })
        .catch(error => {
          console.log(error.message);
        });
    },
    refreshPacientes() {
      this.obterPacientes();
      this.currentPaciente = null;
      this.currentIndex = -1;
    },
    selecionarPaciente(paciente, index) {
      this.currentPaciente = paciente;
      this.currentIndex = index;
    },
    removerTodosPacientes() {
      PacienteWS.deletarTodosPacientes()
        .then(response => {
          console.log(response.data);
          this.refreshPacientes();
        })
        .catch(error => {
          console.log(error.message);
        });
    }
  },
  mounted() {
    this.obterPacientes();
  }
};
</script>

<!-- ESTILIZAÇÃO -->

<style>
.list {
  text-align: left;
  max-width: 750px;
  margin: auto;
}
</style>