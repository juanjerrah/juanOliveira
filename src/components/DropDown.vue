<template>
    <div class="q2">
        <div class="question-title">Questão 2</div>
        <div class="question-title">Dropdown:</div>
        <div class="question-text">
            Transforme a estrutura dada em um seletor dropdown (como um <tt>&#60;select/&#62;</tt>)
            a partir das opções dadas em <tt>:opcoesDD</tt>, indicando a opção atualmente selecionada
            no texto do seletor e visualmente na lista de opções. A opção padrão deve ser inicialmente
            a primeira opção dada na lista. Crie também uma função que retorne a opção selecionada no
            formato <tt>[ texto, idx ]</tt> ('texto' sendo a opção em si, e 'idx' seu índice na lista)
            para leitura pelo componente pai.
        </div>
        <div class="dropSpace" >
            <div class="dropdown" @click.stop.prevent="handleToggleOpen()"> {{ opcaoSelecionada }} ⬇ </div>
            <ul v-show="isOpened">
                <!-- OPÇÕES PASSADAS (INDICANDO A ATUAL SELECIONADA) -->
                <li 
                    class="list" 
                    @click.stop.prevent="pega(item)" 
                    v-for="item in opcoesDD" 
                    :key="item.id"
                >
                    {{ item }}
                </li> 
            </ul>
        </div>
    </div>
</template>

<script>
    export default {
        name: "DropDown",
        props: {
            opcoesDD: Array
        },
        data() {
            return {
                opcaoSelecionada: 'Select',
                isOpened: false
            };
        },
        methods: {
            // Permitir ler dados...
            handleToggleOpen: function(){
                this.isOpened = !this.isOpened;   
            },
            pega:function(opc){
                this.opcaoSelecionada = opc;
                this.handleToggleOpen();
            }
        },
        // Atualizar dados com opções passadas...
    }
</script>

<style scoped>
    .q2{
        border: 1px solid #000;
        border-radius: 7px;
        padding:10px;
    }
    .dropSpace{
        width: fit-content;
    }
    .dropdown {
        cursor: pointer;
        border: 1px solid #2c3e50;
        border-radius: 5px;
        width: fit-content;
        padding: 5px;
        position: relative;
        top: 12px;
        margin-bottom: 12px;
        background: #fff;
    }
    .list{
        list-style-type: none;
        border-bottom: 1px solid #ccc;
        margin-bottom: 5px;
        cursor: pointer;
        border-radius: 5px 5px 0 0;
        padding: 5px;
        font-size: 15px;
        
    }
    .list:hover{
        background-color: purple;
        color: #fff;
    }
    
    ul{
        width: 150px;
        height: 200px;
        padding: 3px 10px;
        border: 1px solid #2c3e50;
        border-radius: 5px;
        overflow-y: scroll;
        background: #fff;
    }
    ul::-webkit-scrollbar {
        width: 10px;               /* width of the entire scrollbar */
    }
    ul::-webkit-scrollbar-track {
        background: #eee;        /* color of the tracking area */
    }

    ul::-webkit-scrollbar-thumb {
        background-color: purple;    /* color of the scroll thumb */
        border-radius: 5px;       /* roundness of the scroll thumb */
          /* creates padding around scroll thumb */
    }   
</style>
