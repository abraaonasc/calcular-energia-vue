<template>
    <v-form v-model="valid">
           <v-text-field
           :rules="rules.fieldsFirstRules"
            v-model="numberFisrt"
            label="Ultimo valor medido na conta de luz"
            required
            v-mask="'####'"
            ></v-text-field>

            <v-text-field
                :rules="rules.fieldsLastRules"
                v-model="numberLast"
                label="Valor atual no seu relogio"
                required
                  v-mask="'####'"
            ></v-text-field>

            <v-text-field
                :rules="rules.filedkwhRules"
                v-model="kwh_atual"
                label="Valor atual do kwh na sua cidade"
                required
                 v-mask="'#.##'"
            ></v-text-field>

            <v-text-field
                v-model="result"
                label="Valor da sua conta"
                required
                disable 
                disabled=true
            ></v-text-field>

            <v-text-field
                v-model="kwh_consumo"
                label="consumo"
                required
                disabled=true
            ></v-text-field>

   
           <v-btn
            :disabled="!valid || null"
            @click="calcularConta"
            class="salvar-btn"
              x-large
              dark
                color="primary"
            >
             Calular
    </v-btn>
        <v-btn
          x-large
          class="white--text ma-5"
        >
          salvar 
        </v-btn>
    </v-form>
</template>


<script>
import {mask} from 'vue-the-mask'
// import Vuetify from 'vuetify'
export default {
    name: 'Form',
    data(){
        return{
            valid:true,
            numberFisrt :null,
            numberLast : null,
            kwh_atual:null,
            kwh_consumo:null,
            result:null,

            rules:{
                fieldsFirstRules: [
                    v => !!v || 'Esse campo é necessário para o calculo',
                ],
                fieldsLastRules: [
                    v => !!v || 'Esse campo é necessário para o calculo',
                    v => v > this.numberFisrt || 'O numero deve ser maior que o ultimo valor medido',
                ],
                filedkwhRules: [
                    v => !!v || 'O valor do KWh é necessário para concluir o cáclulo',
                ],
                }
        }
    },
    directives: {mask},

    methods:{   
        calcularConta:function(){
            this.numberLast = this.numberLast.replace('.',',')

            let result = this.numberLast - this.numberFisrt
            this.kwh_consumo =this.numberLast - this.numberFisrt
            result = result * this.kwh_atual
            this.result = 'R$ ' +result.toFixed(2).replace('.',',') 

            localStorage.setItem('ultimoValor',this.numberFisrt)
        },
    },  
    mounted: function () {
        this.$nextTick(function () {
             if (localStorage.getItem('ultimoValor')!= null){
                let number = localStorage.getItem('ultimoValor')
                number = parseInt(number)
                console.log(number)
                this.numberFisrt = number    
            }
        })
    },
}


</script>


<style scoped>
    form{
        text-align: left;
        max-width: 385px;
        width: 100%;
        margin: 0 10px;
        border: 1px solid #ccc;
        border-radius: 0px 0px 16px 16px;
        padding: 20px;
    }
    .v-text-field__slot {
        padding: 9px 20px 0px 20px;
    }

    .v-btn{
        background: red;
    }

    .salvar-btn{
        background-color: green  !important;
        margin-right: 30px;
    }
    .theme--dark.v-btn.v-btn--disabled.v-btn--has-bg {
        background-color: #ccc !important;
        color: #fff !important;
    }
</style>

<style>
    .v-messages__message {
        color: red !important;
    }
</style>
