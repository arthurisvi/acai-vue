<template>
<div>
    <p>Componente de mensagem</p>
    <div>
        <form id="acai-form">
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
                   <input type ="checkbox" name = "fruits" :value="fruit.tipo" v-model="fruits">
                    <span>{{ fruit.tipo }}</span>
                </div>
            </div>
            <div id = "optional-container" class = "input-container">
                <label id = "optional-title" for="complement">Escolha 1 ou mais complementos: </label>
                <div class = "checkbox-container" v-for="complement in complements" :key="complement.id">
                   <input type ="checkbox" name = "complements" :value="complement.tipo" v-model="complements">
                    <span>{{ complement.tipo }}</span>
                </div>
            </div>
            <div class = "input-container">
                <input type ="submit" class = "submit-btn" value="Montar açaí">
            </div>
        </form>
    </div>
</div>

</template>

<script>

export default{
    name: 'Form',
    data(){
        return{
            sizes: null,
            fruits: null,
            complements: null,
            cupSize: null, 
            fruit: [],
            complement: [],
            status: "Solicitado",
            message: null
        }
    }, methods:{
        async getIngredients(){
            const req = await fetch("http://localhost:3000/ingredients");
            const data = await req.json();

            this.sizes = data.sizes
            this.fruits = data.fruits
            this.complements = data.complements
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

    .submit-btn{
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
    }



</style>
