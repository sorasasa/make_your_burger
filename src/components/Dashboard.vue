<template>
<div id="burger-table">
    <Message :msg="msg" v-show="msg"/>
    <div>
        <span id="burger-table-heading">
            <span class="order-id">#</span>
            <span>Cliente:</span>
            <span>Pão:</span>
            <span>Carne:</span>
            <span>Opcionais:</span>
            <span>Ações:</span>
        </span>
    </div>
    <span id="burger-table-rows">
        <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
            <span class="order-number">{{ burger.id }}</span>
            <span>{{ burger.nome }}</span>
            <span>{{ burger.pao }}</span>
            <span>{{ burger.carne }}</span>
            <span>
                <ul>
                    <li v-for="(opcional,index) in burger.opcionais" :key="index">
                      {{ opcional }}
                    </li>
                </ul>
            </span>
            <div>
            <select name="status" class="status" @change="updateBurger($event, burger.id)">
                <option value="">Selecione</option>
                <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">
 <!--se o tipo for igual ao status do burger vai selecionar a opção-->
                {{ s.tipo }}
                </option>
            </select><!--ta em loop o burger.id-->
            <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
            </div>
        </div>

    </span>
</div>
</template>
<script>
import Message from "./Message.vue" 

export default {
    name: 'Dashboard',
    data(){
        return {
            burgers: null,
            burger_id: null,
            status:[],
            msg: null
        }
    },
    components: {
        Message
    },
    methods: {
        async getPedidos() {
/**requirido e vai esperar */
            const req = await fetch("http://localhost:3000/burgers");
/**vai transformar em json */
            const data = await req.json();
/**os dados vao pra this.burgers */
            this.burgers = data;
/**resgatar os status */
           this.getStatus();
        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;

            console.log(data);
        },
        async deleteBurger(id){
/**muda o metodo da requisição */
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });
            const res = await req.json();

            this.msg = `Pedido removido com sucesso!`;
            //limpar msg
            setTimeout(()=> this.msg = "", 3000);
            

            this.getPedidos(); /**força uma atualização do sistema */
        },//id do hamburger
        async updateBurger(event, id){
/**saber qual o status q ta sendo colocado */
            const option = event.target.value;
/**colocando em string o json de status p atualizar no server */
            const dataJson = JSON.stringify({status : option});
/**acessa pelo id e atualiza o status no backend */
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'PATCH', //so atualiza oq foi enviado(status)
                headers:{"Content-Type" : "application/json"},
                body: dataJson
            });

            const res = await req.json();

            this.msg = `O pedido N° ${res.id} foi atualizado para ${res.status}`;
            //limpar msg
            setTimeout(()=> this.msg = "", 3000);

            console.log(res);
        }
    },
    mounted() {
        this.getPedidos();
    }

}
</script>
<style scoped>

#burger-table {
    max-width: 1200px;
    margin: 0 auto; /**centraliza a tablela no centro */
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row{
    display: flex;
    flex-wrap: wrap; /**um do lado do outro horizontal */
}

#burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333; /**linha embaixo dos nomes */
}

.burger-table-row span,
#burger-table-heading span {
    width: 19%;
}

.burger-table-row {
    width: 100%;
    padding: 14px;
    border-bottom: 1px solid #ccc;
}

#burger-table-heading .order-id,
.burger-table-row .order-number{
    width: 5%;
}

select{
    padding: 12px 4px;
    margin-right: 12px;
}
.delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}
.delete-btn:hover {
    background-color: transparent;
    color: #222;
}

</style>