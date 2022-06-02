<template>
    <div class="page">

        <div class="menu">

            <a href="#"><img src="../assets/back.png" class="back"/></a>
            <a href="#"><img src="../assets/user.png" class="user_img"/></a>

        </div>
        <div class="body_page">
            <h1 class="nome_aluno">Nome do Aluno</h1>
            <div class="info_user">
                <ul class="opcoes">
                    <img src="../assets/config.png" class="img_opcao"/>
                    <li class="opcao"><a href="#">Telefone</a></li>
                </ul>
                <ul class="opcoes">
                    <img src="../assets/info.png" class="img_opcao"/>
                    <li class="opcao"><a href="#">Email</a></li>
                </ul>
                <ul class="opcoes">
                    <img src="../assets/sair.png" class="img_opcao"/>
                    <li class="opcao"><a href="#">Senha</a></li>
                </ul>
            </div>
            <div class="info_app">
                 <ul class="opcoes">
                    <img src="../assets/exclamacao.png" class="img_opcao"/>
                    <li class="opcao"><a href="#">Avaliação</a></li>
                </ul>
                <ul class="opcoes">
                    <img src="../assets/config.png" class="img_opcao"/>
                    <li class="opcao"><a href="#">Configurações</a></li>
                </ul>
                <ul class="opcoes">
                    <img src="../assets/info.png" class="img_opcao"/>
                    <li class="opcao"><a href="#">Jurídico</a></li>
                </ul>
                <ul class="opcoes">
                    <img src="../assets/sair.png" class="img_opcao"/>
                    <li class="opcao"><a href="#">Sair</a></li>
                </ul>

            </div>
        </div>

    </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
    name: "InfoPage",
})
</script>

<style>
*{
    padding: 0;
    margin: 0;
  
}

body{
      background-color: #E5E5E5;
}

li{
    list-style-type: none;
}

a{
    text-decoration:none;
    color: black;
}

.menu{
    width: 100%;
    height: 8vh;
    margin-top: 20px;
}

.back{
    width: 8.5%;
    height: 4vh;
    float: left;
    margin-top: 3%;
    margin-left: 5%;
}

.user_img{
    width: 17%;
    height: 8vh;
    float: right;
    border-radius: 50px;
    margin-right: 15px;
}

.nome_aluno{
    width: 95%;
    font-size: 50px;
    margin-left: 5%;
    margin-top: 5%; 
}

.info_user{
    position: relative;
    margin-top: 40px;
}

.opcoes{
    width: 100%;
    height: 8vh;
    background-color: white;   
    
}

.opcao{
    position: relative;
    top: 50%;
    transform: translateY(-50%);
    margin-left: 25px;
}

.img_opcao{
    width: 1.4rem;
    float: left;
    position: relative;
    top: 50%;
    transform: translateY(-50%);
    margin-left: 25px;
    margin-right: 10px;
}

.info_app{
    position: relative;
    margin-top: 40px;
}
</style>