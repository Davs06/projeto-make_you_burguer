<template>
    <div>
        <p>message component</p>
        <form action="" id="burguer-form">

            <div class="input-container">
                <label for="nome">Nome:</label>
                <input type="text" name="nome" id="nome" v-model="nome" placeholder="Digite seu Nome">
            </div>

            <div class="input-container">
                <label for="pao">Escolha o pão</label>
                <select name="pao" id="pao" v-model="pao">
                    <option value="" selected>Selecione seu Pão</option>
                    <option value="">Integral</option>
                    <option value="">Brioche</option>
                    <option value="">Australiano</option>
                </select>            
            </div>

            <div class="input-container">
                <label for="carne">Escolha a carne</label>
                <select name="carne" id="carne" v-model="carne">
                    <option value="" selected>Selecione a carne</option>
                    <option value="">Costela</option>
                    <option value="">Pichanha</option>
                    <option value="">Alcatra</option>
                </select>            
            </div>

            <div class="input-container" id="opcionais-container">
                <label id="opcionais-title" for="opcionais">Escolha os opcionais</label>
                <div class="checkbox-container">
                    <input type="checkbox" name="opciionais" v-model="opcionais" value="bacon">
                    <span>Bacon</span>
                </div>    
                
                <div class="checkbox-container">
                    <input type="checkbox" name="opciionais" v-model="opcionais" value="bacon">
                    <span>Chadder</span>
                </div> 

                <div class="checkbox-container">
                    <input type="checkbox" name="opciionais" v-model="opcionais" value="bacon">
                    <span>Parmesao</span>
                </div> 
            </div>

            <div class="input-submit">
                <input type="submit" value="Criar meu Burguer" class="submit-btn">
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name:"BurguerForm"
}
</script>

<style scoped>

#burguer-form{
    max-width: 400px;
    margin: 0 auto;
}

.input-container{
    display: flex;
    flex-direction: column;
    margin-top: 50px;
}

label{
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba09;
}

input,select{
    padding: 5px 10xp;
    width: 300px;
    height: 30px;
    border-radius: 5px;
}

#opcionais-container{
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionais-title{
    width: 100%;
}

.checkbox-container{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span, .checkbox-container input{
    width: auto;
}

.checkbox-container span{
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn{
    background-color: #222;
    color: #fcba09;
    font-weight: bold;
    border:  2px solid #222;
    padding: 0 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover{
    background-color:  transparent;
    color: #222;
}

</style>