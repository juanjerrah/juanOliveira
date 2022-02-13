<template>
    <div class="q1">
        <div class="question-title">Questão 1</div>
        <div class="question-title">Processamento de senha:</div>
        <div class="question-text">
            Crie funções de conferência para cada elemento necessário à entrada de senha
            (ao menos um caractere minúsculo, ao menos 8 caracteres, senhas iguais, etc...)
            e exiba os pontos conferidos apenas quando o usuário começar a digitar na caixa
            de texto.
        </div>

        <div class="form-group">
            <label for="senha"> <span> Senha: </span> </label>
            <input v-model="senha" type="password" id="senha" placeholder="Insira sua senha..." required/>

            <label for="senhaConf"> <span> Repita a senha: </span> </label>
            <input v-model="senhaConf" type="password" id="senhaConf" placeholder="Repita a senha..." required/>
        </div>

        <span v-if="showAdvice()" class="senha-err">As duas senhas devem ser iguais!</span>

        <span v-if="placeholder" class="senha-err">
            <ul>
                <li :class="{'conferido': hasLower()}">Pelo menos um caractere minúsculo</li>
                <li :class="{'conferido': hasUpper()}">Pelo menos um caractere maiúsculo</li>
                <li :class="{'conferido': hasSpecialChar()}">Pelo menos um caractere especial</li>
                <li :class="{'conferido': hasNumber()}">Pelo menos um caractere numérico</li>
                <li :class="{'conferido': handleLength()}">Pelo menos oito caracteres</li>
            </ul>
        </span>
    </div>
</template>

<script>
    export default {
        name: "Senha",
        data() {
            return {
                senha: "",
                senhaConf: "",   
            }
        },

        computed: {

            placeholder() {
                let mostra = false;
                if(this.hasLower() && this.hasUpper() && this.handleLength() && this.hasNumber() && this.hasSpecialChar()){
                    mostra = false;
                }else{
                    if(this.senha.length > 0){
                        mostra = true;
                    }
                }
                return mostra;
            },
            

        },

        methods: {
            comparePasswords: function() {
                if (this.senha === this.senhaConf) {
                    return true
                }else{
                    return false
                }
            },
            showAdvice: function(){
                return this.senhaConf != this.senha && this.senhaConf != '' ;
            },

            handleLength(){
                return this.senha.length >= 8;
            },
            hasLower(){
                for(let i = 0; i< this.senha.length; i++){
                    if(this.senha[i] == this.senha[i].toLowerCase()){
                        return true;
                    }
                }
            },
            hasUpper(){
                for(let i = 0; i< this.senha.length; i++){
                    if(this.senha[i] == this.senha[i].toUpperCase()){
                        return true;
                    }
                }
            },
            hasSpecialChar(){
                const regExp = /[@!#$%.^&[\]*()/\\]/;
                return regExp.test(this.senha)
            },
            hasNumber(){
                const regExp = /[0-9]/;
                return regExp.test(this.senha)
            }
        }
    }
</script>

<style scoped>
.q1{
    border: 1px solid #000;
    border-radius: 7px;
    margin-bottom: 10px;
    padding: 10px;
}
    .form-group {
        display: grid;
        margin: 0 auto;
        grid-template-columns: auto 1fr;
        grid-template-rows: auto;
        grid-column-gap: 20px;
        grid-row-gap: 5px;
        width: 80%;
        margin-bottom: 5px;
    }

    @media query screen and (max-width: 800px) {
        .form-group {
            width: calc(100% - 20px);
        }
    }
        .form-group{
        display: flex;
        flex-direction: column;
        }
    .form-group > label {
        display: flex;
        justify-content: center;
        align-content: center;
        flex-direction: column;
    }

    .form-group > label > span {
        width: 100%;
        /*text-align: right;*/
    }

    .form-group > input {
        border: 1px solid grey;
        border-radius: 5px;
        width: 200px;
        height: 25px;
        padding-left: 5px;
        outline: none;
        
    }
    .form-group > input:focus{
        border: 1px solid blue;
        box-shadow: 0 0 5px blue;
    }
    

    .conferido {
        color: green !important;
    }

    .senha-err {
        color: red;
    }

    li{
        list-style-type: none;
        font-size: 12px;
    }
    
 
</style>
