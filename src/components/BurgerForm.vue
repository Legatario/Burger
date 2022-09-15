<template>
    <div>
        <Message :msg ="msg" v-show="msg"/>
        <div>
            <form id="burger-form" @submit="createBurger">
                <div class="input_container">
                    <label for="nome">Nome do cliente: </label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
                </div>
    
                <div class="input_container">
                    <label for="pao">Escolha o pão: </label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option :value="pao.tipo" v-for="pao in paes" :key="pao.id">{{ pao.tipo }}</option>
                    </select>
                </div>
    
                <div class="input_container">
                    <label for="carne">Escolha a carne do seu burger: </label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option :value="carne.tipo" v-for="carne in carnes" :key="carne.id" >{{ carne.tipo }}</option>
                    </select>
                </div>
    
                <div class="input_container opcionais_container">
                    <label for="opcionais" id="opcionais-title">Escolha os opcionais: </label>
                    <div class="checkbox_container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" id="opcionais" name="opcionais" v-model="opcionais" :value="opcional.tipo"/>
                        <span>{{ opcional.tipo }}</span>
                    </div>
                </div>
    
                <div class="input_container">
                    <input type="submit" class="submit_btn" value="Criar meu Burger"/> 
                </div>
            </form>

        </div>
    </div>
</template>

<script>
import Message from './Message.vue';
    export default{
    name: "BurgerForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: null
        };
    },
    methods: {
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
            console.log(data);
        },
        async createBurger(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            };
            const dataJson = JSON.stringify(data);
            const req = await fetch(" http://localhost:3000/burgers", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: dataJson
            });

            const res = await req.json();
            
            //colocar msg de sistema
            this.msg = `Pedido nº ${res.id} realizado com sucesso`;

            //limpa msg
            setTimeout(()=> this.msg = "", 3000)

            // limpa cache
            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = "";
        }
    },
    mounted() {
        this.getIngredientes();
    },
    components: { Message }
}
</script>

<style scoped>
    #burger-form{
        max-width: 400px;
        margin: 0 auto;
    }

    .input_container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }
    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #fcba03 ;
    }

    input, select{
        padding:  5px 10px;
        width: 300px;
    }

    .opcionais_container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title{
        width: 100%;
    }

    .checkbox_container{
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox_container span,
    .checkbox_container input{
        width: auto;
    }

    .checkbox_container span{
        margin-left: 6px;
        font-weight: bold;
    }

    .submit_btn{
        background: #222;
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        font-size: 16px;
        cursor: pointer;
        padding: 10px;
        transition: .5s;
    }

    .submit_btn:hover{
        background: transparent;
        color: #222;
    }

</style>