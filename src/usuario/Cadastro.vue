<template>
    <div id="usuario">       
        <h5>{{titulo}} </h5>
        <form @submit.prevent="AdicionarUsuario()">          
            <input  id="nome" v-validate data-vv-rules="required" placeholder="Nome" @input="nome = $event.target.value" :value="nome"><br>
            <input id="telefone" placeholder="Telefone" @input="telefone = $event.target.value" :value="telefone"><br>
            <input id="email" placeholder="E-mail" @input="email = $event.target.value" :value="email"><br>
            <button type="submit">Adicionar</button>
        </form>
        <h5> Interessados </h5>
        
        <table>
            <tr class="cor_fundo">
                <th> Nome </th>
                <th> Telefone </th>
                <th> E-mail </th>
                <th> Ação </th>
            </tr>            
            <tr v-for="(u,i) in usuarios" :key="u._id">
                <th>{{u.nome}}</th>
                <th>{{u.telefone}}</th>
                <th>{{u.email}}</th>
                <th class="ajuste_tamanho"> 
                    <button @click="RemoverUsuario(i)">Remover</button>
                </th>
            </tr>
        </table>       
    </div>
</template>

<script>
import Usuario from '../model/Usuario';
export default {
    data(){
        return{
            titulo:'Cadastro de interesse', 
            nome:'',
            telefone:'',
            email:'',
            usuarios:[]              
        }
    },   
    methods:{
        AdicionarUsuario(){
            let usuario = new Usuario(this.nome,this.telefone,this.email);
            this.usuarios.push(usuario);
            localStorage.setItem('usuarios', JSON.stringify(this.usuarios));
            this.nome='';
            this.telefone='';
            this.email='';
        },
        RemoverUsuario(i){         
            this.usuarios.splice(i,1);
            localStorage.setItem('usuarios',JSON.stringify(this.usuarios));
        }
    }
}
</script>

<style>
#usuario {
    width: 50%;    
}
#usuario form input{
    margin-top: 2%;
    width: 35%;
}
h5{
    margin:0;
    padding: 0;
    font-size: 16px;  
    margin-top: 5%;    
}
table {
  margin-top:3%;
  width: 100%;
  border: 1px solid darkgrey;
  border-collapse: collapse;
  font-size: 14px;
}
tr{
    text-align: left;   
    margin-left: 12%;
    width: 30%;
}
table tr.cor_fundo{
    background:darkgray;
}
.ajuste_tamanho{
    width: 10%;
}
tr:nth-child(odd) {
  background-color: #e6f2ff;
}
button{
    margin-top: 2%;
}
</style>