<template>
    <div id = "acai-table">
        <Message :msg="msg" v-show="msg" />
        <div>
            <div id="acai-table-heading">
                <div class ="order-id">N°</div>
                <div>Copo</div>
                <div>Frutas</div>
                <div>Complemento</div>
                <div>Status</div>
            </div>
        </div>
        <div id="acai-table-rows">
            <div class="acai-table-row" v-for="acai in listAcai" :key="acai.id" >
                <div class="order-number">{{ acai.id }}</div>
                <div>{{ acai.cupSize }}</div>
                <div>
                    <ul>
                        <li v-for="(fruit, idx) in acai.fruit" :key="idx">
                            {{ fruit }}
                        </li>
                    </ul>
                </div>
                <div>
                    <ul>
                         <li v-for="(complement, idx) in acai.complement" :key="idx">
                            {{ complement }}
                        </li>
                    </ul>
                </div>
                <!-- change é para quando houver uma mudança -->
                <select name="status" class="status" @change="updateAcai($event, acai.id)">
                     <option :value="status.tipo" v-for="status in listStatus" :key="status.id" :selected="acai.status == status.tipo">
                    {{ status.tipo }}
                     </option>
                </select>
                <button class="delete-btn" @click="deleteAcai(acai.id)">Cancelar</button>
            </div>
        </div>
    </div>

</template>

<script>
import Message from './Message'

export default{

    name: 'Dashboard',
    components:{
        Message
    },
    data(){
        return{
            listAcai: null,
            acai_id: null,
            listStatus: [],
            msg: null
        }
    }, methods:{

        async getPedidos(){
            const req = await fetch("https://api-acai.herokuapp.com/listAcai")

            const data = await req.json()

            this.listAcai = data


        }, 
        async getStatus(){
            const req = await fetch("https://api-acai.herokuapp.com/status")

            const data = await req.json()

            this.listStatus = data

        },
        async deleteAcai(id){
            const req = await fetch(`https://api-acai.herokuapp.com/listAcai/${id}`, {
                method: "DELETE"
            })

            const res = await req.json()

            this.msg = `Pedido cancelado com sucesso!`
            setTimeout(() => this.msg = "", 2000)

            this.getPedidos()

        },
        async updateAcai(event, id){
            const option = event.target.value
            
            const data = JSON.stringify ({ status: option })

            const req = await fetch(`https://api-acai.herokuapp.com/listAcai/${id}`, { 
                method: "PATCH",
                headers: { "Content-Type": "application/json"},
                body: data
            })

            const res = await req.json()

            this.msg = `O status do pedido N° ${res.id} foi alterado para ${res.status}.`
            setTimeout(() => this.msg = "", 2000)
        }
    }, mounted(){
        this.getPedidos()
        this.getStatus()
    }
}

</script>

<style scoped>

#acai-table{
    max-width: 1200px;
    margin: 0 auto;
}

#acai-table-heading, 
#acai-table-rows,
.acai-table-row{
    display: flex;
    flex-wrap: wrap;

}

#acai-table-heading{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #4C2D51;
}

#acai-table-heading div, 
.acai-table-row div{
    width: 19%
}

.acai-table-row{
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
}

#acai-table-heading .order-id, 
.acai-table-row .order-number{
    width: 5%
}

select{
    padding: 12px 6px;
    margin-right: 12px;
}

.delete-btn{
   background-color: #4C2D51;
        color: #fff;
        font-weight: bold;
        border: 2px solid #4C2D51;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
}

</style>