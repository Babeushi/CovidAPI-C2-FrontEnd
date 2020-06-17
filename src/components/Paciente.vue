<template>
    <div v-if="currentPaciente" class="size edit-form addEdit">
        <h4>Paciente</h4>
        <form>
            <div class="form-group">
                <label for="nome">Nome</label>
                <input type="text" class="form-control" id="nome" v-model="currentPaciente.nome">
            </div>
            <div class="form-group">
                <label for="estado">Estado</label>
                <input type="text" class="form-control" id="estado" v-model="currentPaciente.estado">
            </div>
            <div class="form-group">
                <label for="cidade">Cidade</label>
                <input type="text" class="form-control" id="cidade" v-model="currentPaciente.cidade">
            </div>
            <div class="form-group">
                <label for="endereco">Endereço</label>
                <input type="text" class="form-control" id="endereco" v-model="currentPaciente.endereco">
            </div>
            <div class="form-group">
                <label for="telefone">Telefone</label>
                <input type="text" class="form-control" id="telefone" v-model="currentPaciente.telefone">
            </div>
            <div class="form-group">
                <label for="altura">Altura</label>
                <input type="number" class="form-control" id="altura" v-model="currentPaciente.altura">
            </div>
            <div class="form-group">
                <label for="peso">Peso</label>
                <input type="number" class="form-control" id="peso" v-model="currentPaciente.peso">
            </div>
            <div class="form-group">
                <label for="prob_saude">Problema de saúde</label>
                <input type="text" class="form-control" id="prob_saude" v-model="currentPaciente.prob_saude">
            </div>
        </form>
        <button class="btn mr-2" style="background: #cc66ad;
  color: #fff;" @click="deletarPaciente">Deletar Paciente</button>
        <button type="submit" class="btn  mr-2" style="background: #cc66ad;
  color: #fff;" @click="atualizarPaciente">Atualizar Paciente</button>
    </div>
    <div v-else>
        <p>
            Por favor, selecione um paciente!!!
        </p>
    </div>
</template>

<script>

    import PacienteWS from "../services/PacientesWS";

    export default {
        name: "paciente",
        data(){
            return {
                currentPaciente: null
            }
        }, 
        methods: {
            getPaciente(id){
                PacienteWS.getPacienteID(id)
                    .then(paciente => {
                        this.currentPaciente = paciente.data;
                    })
                    .catch(error => {
                        console.log(error);
                    });
            },
            deletarPaciente(){
                alert("Paciente deletado com sucesso")
                PacienteWS.deletarPacienteID(this.currentPaciente.id)
                    .then(response => {
                        console.log(response.data);
                    })
                    .catch(error => {
                        console.log(error.message);
                    })
                window.location.replace("http://localhost:8081/pacientes")
            },
            atualizarPaciente(){
                alert("Paciente atualziado com sucesso")
                PacienteWS.atualizarPaciente(this.currentPaciente.id, this.currentPaciente)
                    .then(response => {
                        console.log(response.data);
                        this.message = "Paciente atualizado com sucesso!"
                    })
                    .catch(error => {
                        console.log(error.message);
                    })
                window.location.replace("http://localhost:8081/pacientes")
            }
        },
        beforeMount(){
            this.message = '',
            this.getPaciente(this.$route.params.id);
        }
    }
</script>

<style>

</style>