<template>
    <div class="containerPesquisar" >
        <input v-model="dadoPais" type="text" placeholder="Pesquisar Pais">
        <button @click="validarDado(dadoPais)">Presquisar</button>
    </div>
</template>

<script>
import { bus } from '../main'

export default {
    name:'pesquisar',
    data(){
        return{
            dadoPais: null
        }
    },
    methods:{
        pesquisarDado(dado){
            bus.$emit('eventoDadoPais', dado);
        },
        mostrarTodosPaises(){
            bus.$emit('eventoDadoPaisNull');
        },
        limparEspaços(dado){
            return dado.trim();
        },
        verificarExistenciaDado(dado){
            return ((dado == null || dado == '' || dado == ' ') ? false : true );
        },
        converterCaixaBaixa(dado){
            return dado = dado.toLowerCase();
        },
        validarDado(dado){
            (this.verificarExistenciaDado(dado) == true) ? dado = this.converterCaixaBaixa(this.limparEspaços(dado)) : '';
            (this.verificarExistenciaDado(dado) == true) ? this.pesquisarDado(dado) : this.mostrarTodosPaises();
        }
    },
    watch:{
        dadoPais(){
            this.validarDado(this.dadoPais);
        }
    }
}
</script>

<style scooped>
.containerPesquisar{
    display: flex;
    width: 100%;
    justify-content: center;
    margin-bottom: 50px;
}   
input{
    width: 65%;
    height: 50px;
    font-size: 1rem;
    padding: 0 10px;
    box-sizing: border-box;
    border-radius: 10px 0px 0px 10px;
}
button{
    width: 15%;
    font-size: 1rem;
    border: none;
    background-color:#6ae9a3;
    border-radius: 0px 10px  10px 0px;
    transition-duration: 0.5s;
}
button:hover{
    cursor: pointer;
    background-color:  #89f1b8;
}
@media screen and (min-width: 542px) and (max-width: 690px){
    .containerPesquisar{
        margin-bottom: 40px;
    }
    input{
        width: 75%;
        font-size: 0.8rem;
        height: 45px;
    }
    button{
        width: 20%;
        font-size: 0.8rem;
        height: 45px;   
    }
}
@media screen and (max-width: 541px){
    .containerPesquisar{
        margin-bottom: 40px;
    }
    input{
        width: 330px;
        height: 40px;
        font-size: 0.7rem;
    }
    button{
        width: 80px;
        height: 40px;
        font-size: 0.7rem;
    }
}
@media screen and (max-width: 300px) and (max-width: 475px){
    .containerPesquisar{
        margin-bottom: 40px;
    }
    input{
        width: 230px;
        height: 40px;
        font-size: 0.7rem;
    }
    button{
        width: 70px;
        height: 40px;
        font-size: 0.6rem;
    }
}
</style>