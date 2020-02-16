<template>
  <div class="central">
  <section class="secao"><!-- Padrão de código BEM(Block.Element.Modifier), seria legal pesquisar -->
    <header class="secao__header">
      <div class="container">
        <section class="banner">
            <h1>GITHUB API CRAWLER</h1>
            <h2>Um jeito mais facil de recuperar dados da API do GitHub</h2>
            <button>FIND OUT MORE</button>
        </section>
        </div>
    </header>
    <main v-if='nome!= null' class="item secao__main">
        <div class="container">
            <div class="itens nome">
                <img src="../assets/name.png" alt="nameimg" >
                <p>NOME</p>
                {{nome}}
            </div> 
            <div class="itens login">
                <img src="../assets/login.png"  alt="loginimg" >
                <p>LOGIN</p>
                {{login}}
            </div>
            <div class="itens repositorio">
                <img src="../assets/repositorio.png" alt="repositorioimg">
                <p>REPOSITÓRIOS PÚBLICOS</p>
                {{repositorio}} repositórios
            </div>

            <div class="itens seguidores">
                <img src="../assets/seguidores.png" alt="seguidoresimg">
                <p>SEGUITORES</p>
                {{seguidores}} seguidores
            </div>
            <div class="itens empresa">
                <img src="../assets/empresa.png" alt="empresaimg">
                <p>EMRPESA</p>
                {{empresa}}
            </div>
            <div class="itens site">
                <img src="../assets/site.png" alt="some text">
                <p>SITE</p>
                <a :href="site">{{site}}</a>
            </div>

            <div class="avatar">
                <div class="infoavatar">
                    <div class="avatarimg">
                        <img :src="avatar" alt="foto"> 
                    </div>
                    <p class="nomeavatar">{{nome}}</p>
                    <p class="loginavatar">{{login}}</p>
                    <p class="infobio">{{bio}}</p>
                </div>
            </div>

            <div class="itens bio">
                <div>
                    
                </div>
            </div> 
        </div>
    </main>
    <div v-else class="erro">
        <div class="error">
            <h1>USUARIO NÃO ENCONTRADO</h1>
        </div>
    </div>

    
    <footer class="secao__footer">
        <div class="container">
            <div class="footerfundo">
                <img src="../assets/GitHub.png" alt="">
            </div>
            <div class="text-footer">
                <p class = "textfooter">O Github API Crawler serve para procurar por 
                    desenvolvedores por meio da API do Github</p>
                <p class = "textfooter2" >PENSANDO COM CARINHO POR LUCCAS PIOLA</p>
            </div>
        </div>
    </footer>
  </section>
  </div>

</template>

<script>
import axios from 'axios';
import usuario from '../services/usuario';

export default {
    name: 'home',
    data () {
    return {
      nome: null,
      login: 'Vazio',
      repositorio: 0,
      seguidores: 0,
      empresa: 'Vazio',
      site: 'Nenhum Site Disponivel',
      avatar: 0,
      bio: 'Nenhuma biografia encontrada',
    }
  },
  mounted () {
    axios
      .get(`https://api.github.com/users/${usuario}`)
      .then(response => (this.nome = response.data.name) +
      (this.login = response.data.login) + 
      (this.repositorio = response.data.public_repos)+
      (this.seguidores = response.data.followers)+
      (this.empresa = response.data.company)+
      (this.site = response.data.blog)+
      (this.avatar = response.data.avatar_url)+
      (this.bio = response.data.bio)
      )
  },
    
}
</script>

<style>
    @import '../components/footer.css';
    @import '../components/banner.css';
    @import '../components/skeleton.css';
    @import '../components/infoUser.css';
</style>