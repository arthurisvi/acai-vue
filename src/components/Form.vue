<template>
<div>
    <p>Componente de mensagem</p>
    <div>
        <form id="acai-form">
            <div class = "input-container">
                <label for="fruits">Escolha o tamanho do copo: </label>
                <select name="cup-size" id ="cup-size" v-model ="cupSize">
                    <option value = "">Selecione o tamanho em ml</option>
                    <option value = "300">300ml</option>
                    <option value = "500">500ml</option>
                    <option value = "700">700ml</option>
                </select>
            </div>
            <div id = "optional-container"  class = "input-container">
                <label id = "optional-title" for="fruits">Escolha 1 ou mais frutas: </label>
                <div class = "checkbox-container">
                    <input type ="checkbox" id = "fruit-banana" name = "fruit-banana" value = "Banana" v-model="fruits">
                    <span>Banana</span>
                    <!-- <label for="fruit-banana">Banana</label> -->
                    <input type ="checkbox" id = "fruit-kiwi" name = "fruit-kiwi" value = "Kiwi" v-model="fruits">
                    <!-- <label for="fruit-kiwi">Kiwi</label> -->
                    <span>Kiwi</span>
                    <input type ="checkbox" id = "fruit-morango" name = "fruit-morango" value= "Morango" v-model="fruits">
                    <!-- <label for="fruit-morango">Morango</label> -->
                    <span>Morango</span>
                    <input type ="checkbox" id = "fruit-abacaxi" name = "fruit-abacaxi" value= "Abacaxi" v-model="fruits">
                    <!-- <label for="fruit-abacaxi">Abacaxi</label> -->
                    <span>Abacaxi</span>
                </div>
            </div>
            <div id = "optional-container" class = "input-container">
                <label id = "optional-title" for="complement">Escolha 1 ou mais complementos: </label>
                <div class = "checkbox-container">
                    <input type ="checkbox" id = "complement-oreo" name = "complement-oreo" value = "Oreo" v-model="complement">
                    <span>Oreo</span>
                   <!-- <label for="complement-oreo">Oreo</label> -->
                    <input type ="checkbox" id = "complement-condensed" name = "complement-condensed" value = "Leite Condensado" v-model="complement">
                    <!-- <label for="complement-condensed">Leite Condensado</label> -->
                    <span>Leite Condensado</span>
                    <input type ="checkbox" id = "complement-milk" name = "complement-milk" value = "Leite em pó" v-model="complement">
                    <span>Leite em pó</span>
                    <!-- <label for="complement-milk">Leite em pó</label> -->
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
    name: 'Form'

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
