<template>
<div id="main-banner">
    <h1>Make Your Burger</h1>
</div>
</template>
<script>
export default {
    name: 'Banner'
}
</script>
<style scoped>
#main-banner {
    background-image: url('/public/img/burger.jpg');
    background-position: 0 -250px; /**desloca pra cima */
    background-size: cover; /**aproveita melhor o espaço disponivel pra imagem, largura 100% */
    height: 500px;
    display: flex; /**move o h1 */
    align-items: center; /**e alinha no centro vertical */
    justify-content: flex-start; /**alinha a esquerda horizontal */
}
#main-banner h1 {
    color: #FFF; /**cor do texto */
    text-align: center;
    font-size: 60px;
    background-color: #222;
    padding: 20px 40px; /**espaçamento */

}
</style>