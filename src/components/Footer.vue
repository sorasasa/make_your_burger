<template>
  <footer id="footer">
    <p>Make Your Burger &copy; 2023</p>
  </footer>
</template>
<script>
export default {
    name:'Footer',
}
</script>

<style scoped>
   #footer {
    height: 200px;
    background-color: #222;
    border-top: 4px solid #111;
    color: #FCBA03;
    display: flex;
    align-items: center; /**vertical */
    justify-content: center; /**horizontal */
    width: 100%; /**largura */
    position: absolute; /** p grudar no fundo*/

   }
</style>