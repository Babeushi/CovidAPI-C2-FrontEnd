<template>
    <div class="size submit-form addEdit">
        <div class="form-group">
            <label for="nome">Nome</label>
            <input 
                type="text" 
                class="form-control" 
                id="nome" 
                v-model="paciente.nome" 
                name="nome"
            />
        </div>
        <div class="form-group">
            <label for="estado">Estado</label>
            <input 
                type="text" 
                class="form-control" 
                id="estado" 
                v-model="paciente.estado" 
                name="estado"
            />
        </div>
        <div class="form-group">
            <label for="cidade">Cidade</label>
            <input 
                type="text" 
                class="form-control" 
                id="cidade" 
                v-model="paciente.cidade" 
                name="cidade"
            />
        </div>
        <div class="form-group">
            <label for="endereco">Endereço</label>
            <input 
                type="text" 
                class="form-control" 
                id="endereco" 
                v-model="paciente.endereco" 
                name="endereco"
            />
        </div>
        <div class="form-group">
            <label for="telefone">Telefone</label>
            <input 
                type="telefone" 
                class="form-control" 
                id="telefone" 
                v-model="paciente.telefone" 
                name="telefone"
            />
        </div>
        <div class="form-group">
            <label for="altura">Altura</label>
            <input 
                type="number" 
                class="form-control" 
                id="altura" 
                v-model="paciente.altura" 
                name="altura"
            />
        </div>
        <div class="form-group">
            <label for="peso">Peso</label>
            <input 
                type="number" 
                class="form-control" 
                id="peso" 
                v-model="paciente.peso" 
                name="peso"
            />
        </div>
        <div class="form-group">
            <label for="prob_saude">Problema de saúde</label>
            <input 
                type="text" 
                class="form-control" 
                id="prob_saude" 
                v-model="paciente.prob_saude" 
                name="prob_saude"
            />
        </div>
        <button @click="inserirPaciente" class="btn btn-success">
            inserir Paciente
        </button>
    </div>
</template>

<script>

import PacientesWS from '../services/PacientesWS';
    export default {
        name: "adicionarPaciente",
        data(){
            return {
                paciente: {
                    id: "",
                    nome: "",
                    estado: "",
                    cidade: "",
                    endereco: "",
                    telefone: "",
                    altura: 0,
                    peso: 0,
                    prob_saude: ""
                }
            }
        },
        methods: {
            inserirPaciente(){
                let dadosPaciente = {
                    nome: this.paciente.nome,
                    estado: this.paciente.estado,
                    cidade: this.paciente.cidade,
                    endereco: this.paciente.endereco,
                    telefone: this.paciente.telefone,
                    altura: this.paciente.altura,
                    peso: this.paciente.peso,
                    prob_saude: this.paciente.prob_saude
                }
                alert("Paciente cadastrado com sucesso")
                
                PacientesWS.criarPaciente(dadosPaciente)
                    .then(resp => {
                        this.paciente.id = resp.data.id;
                        console.log(this.paciente);
                    }).catch(error => {
                        console.log(error.message);
                    })
                location.reload()
            }
        }
    }
</script>