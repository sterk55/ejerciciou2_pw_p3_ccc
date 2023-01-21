<template>
  <h1>Lista de Estados</h1>
  <table>
    <tr>
        <td><p>{{data1}}</p></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
  </table>
  <table>
    <tr>
        <td><h3>Ingrese la Inicial: </h3></td>
        <td><input  onkeypress="13" v-model="verInfo" type="text" name="iniciales" id="inicialId"></td>
    </tr>
    </table>
    <table>
    <tr>
        <td><button v-on:click="buscar">Buscar</button></td>
    </tr>
    <tr><td><h3>La informacion Final es la Siguiente: </h3></td></tr>
  </table>
  <table>
    <tr>
        <td><p>Casos Positivos: </p></td>
        <td><p>{{ positivos }}</p></td>
    </tr>
    <tr>
        <td><p>Total de Test: </p></td>
        <td><p>{{totalTest}}</p></td>
    </tr>
    <tr>
        <td><p>Hospitalizados: </p></td>
        <td><p>{{hospitalizados }}</p></td>
    </tr>
    <tr>
        <td><p>Muertos: </p></td>
        <td><p>{{ muertos }}</p></td>
    </tr>
    <tr>
        <td><p>Total de Test Viral: </p></td>
        <td><p>{{ totalTestViral }}</p></td>
    </tr>
    <tr>
        <td><p>Aumento de Muertos: </p></td>
        <td><p>{{ muertosAumentados }}</p></td>
    </tr>
  </table>
</template>

<script>
export default {
    data(){
        return{
            state:[],
            inicial:"",
            positivos:null,
            totalTest:null,
            hospitalizados:null,
            muertos:null,
            totalTestViral:null,
            muertosAumentados:null,
            verInfoo:null,
            verInfo:null,
            data1:""
        }

    },
    
    components:{


    },
    methods:{
       async consumirAPIEstado(){
  
        var data = await fetch('https://api.covidtracking.com/v1/states/current.json').then((r)=>r.json())
        this.state = data
        
        console.log(data[0].state)
        this.data1=data[0].state
        
        return data
        },

        async consumirApiInformacion(inicial){
            const {positive, totalTestResults, hospitalizedCurrently, death, totalTestsViral, deathIncrease} = await fetch('https://api.covidtracking.com/v1/states/'+inicial+'/current.json').then((r)=>r.json())

            this.positivos = positive
            this.totalTest = totalTestResults
            this.hospitalizados = hospitalizedCurrently
            this.muertos = death
            this.totalTestViral = totalTestsViral
            this.muertosAumentados = deathIncrease

        },
        buscar(){
            this.consumirApiInformacion(document.getElementById('inicialId').value)
            this.consumirAPIEstado()

        } 
    },
    watch:{
        verInfoo(value){
            
            if(!value.includes()) return;
            console.log("vamos a consumir el API")
           
        },
        verInfo(event){
            console.log(event.key)
            /*if(!value.includes('')) return;
            console.log("vamos a consumir el API")
            this.consumirAPI()*/
        }
        }
    }

</script>

<style>
table{
    margin: 0 auto;
}
</style>