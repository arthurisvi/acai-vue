<template>
<div>
    <!--<Modal />-->
    <div>
        <form id="acai-form" @submit="createAcai"> 
            <div class = "input-container">
                <label for="fruits">Escolha o tamanho do copo: </label>
                <select name="cup-size" id ="cup-size" v-model ="cupSize">
                    <option value = "">Selecione o tamanho em ml</option>
                    <option v-for="size in sizes" :key="size.id" :value = "size.tipo">
                        {{ size.tipo }}
                    </option>
            </select>
            </div>
            <div id = "optional-container"  class = "input-container">
                <label id = "optional-title" for="fruits">Escolha 1 ou mais frutas: </label>
                <div class = "checkbox-container" v-for="fruit in fruits" :key="fruit.id">
                   <input type ="checkbox" name = "fruits" :value="fruit.tipo" v-model="fruitsData">
                    <span>{{ fruit.tipo }}</span>
                </div>
            </div>
            <div id = "optional-container" class = "input-container">
                <label id = "optional-title" for="complements">Escolha 1 ou mais complementos: </label>
                <div class = "checkbox-container" v-for="complement in complements" :key="complement.id">
                   <input type ="checkbox" name = "complements" :value="complement.tipo" v-model="complementsData">
                    <span>{{ complement.tipo }}</span>
                </div>
            </div>
            <ShowModal />
            <!-- <div class = "input-container">
                <input type ="submit" class = "submit-btn" value="Montar açaí">
            </div> -->
        </form>
    </div>
</div>

</template>

<script>

import Modal from './Modal.vue'
import ShowModal from './ShowModal.vue'

export default{
    name: 'Form',
    components:{
        Modal,
        ShowModal
    },
    data(){
        return{
            sizes: null,
            fruits: null,
            complements: null,
            cupSize: null, 
            fruitsData: [],
            complementsData: [],
            message: null
        }
    }, methods:{
        async getIngredients(){
            const req = await fetch("https://api-acai.herokuapp.com/ingredients")
            const data = await req.json()

            this.sizes = data.sizes
            this.fruits = data.fruits
            this.complements = data.complements
        }, 

        async createAcai(e){
            e.preventDefault()

            const data ={
                cupSize: this.cupSize,
                fruit: Array.from(this.fruitsData),
                complement: Array.from(this.complementsData),
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data)

            const req = await fetch("https://api-acai.herokuapp.com/listAcai", {
                method: "POST",
                headers: { "Content-Type": "application/json"},
                body: dataJson
            })

            const res = await req.json();
            
            this.cupSize = ""
            this.fruitsData = ""
            this.complementsData = ""

        }
    }, mounted(){
        this.getIngredients();
    }

}

</script>

<style scoped>
    #acai-form{
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #4C2D51;
        padding: 5px 10px;
        border-left: 4px solid rgb(132, 181, 28, 1);
    }

    input, select{
        padding: 5px 10px;
        width: 300px;
    }

    #optional-container{
        flex-direction: row;
        flex-wrap: wrap;
    }


    #optional-title{
        width: 100%;
    }

    .checkbox-container{
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 5px;
    }

    .checkbox-container span,
    .checkbox-container input{
        width: auto;
    }

    .checkbox-container span{
        margin-left: 6px;
        margin-right: 6px;
        font-weight: bold
    }

    /* .submit-btn{
        background-color: #4C2D51;
        color: #fff;
        font-weight: bold;
        border: 2px solid #4C2D51;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.5s
    }

    .submit-btn:hover{
        background-color: transparent;
        color: rgb(132, 181, 28, 1);
    } */



</style>
