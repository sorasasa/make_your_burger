<template>
<nav><!--ou div#nav-->
    <router-link to="/" id="logo-url">
        <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <router-link to="/">Home</router-link> 
    <router-link to="/pedidos">Pedidos</router-link>
</nav>
</template>
<script>
export default {
    name: 'Navbar',/**imagem vai tirar p exibir o logo && alt seria o nome do projeto**/
    props: ['logo', 'alt'] /**propriedades */
}
</script>
<style scoped>
nav {
    background-color:#222;
    border-bottom: 4px solid #111; /**linha de baixo do nav */
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end; /**joga os itens pro fim do lado direito */
    align-items: center; /**alinha no meio de cima p baixo */
}
nav a {
    color:#FCBA03;
    text-decoration: none; /**nao tem A, mas mesmo assim funcionou pq é um link */
    margin: 12px; /**distancia entre os links */
    transition: .5s;

}
nav a:hover {
    color: #fff
}
#logo-url {
    margin: auto;
    margin-left: 0; /**joga a logo pra esquerda */
}
#logo {
    width: 40px;
    height: 40px;
}
</style>