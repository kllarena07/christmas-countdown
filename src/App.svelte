<script lang="ts">
  import bw_tree from './assets/tree-bw.png'

  let month = 12

  const calculateDaysFromChristmas = () => {
    let today = new Date(`${month}/1/2023`)
    let target_year = today.getMonth() + 1 === 12 && today.getDate() > 25 ? today.getFullYear() + 1 : today.getFullYear()
    let next_christmas = new Date(`12/25/${target_year}`)
    let difference = next_christmas.getTime() - today.getTime()
    return { difference: Math.ceil(difference / (1000 * 3600 * 24)), year: target_year }
  }

  let day_difference = calculateDaysFromChristmas().difference
  let year = calculateDaysFromChristmas().year

  let tree_height = `${(((365 - day_difference) / 365) * 473) * 0.93}px`
</script>

<main>
  <section id="app-container">
    <div id="mask-container">
      <img src={bw_tree} width="500" height="473" alt="bw tree" />
      <div id="colored-tree" style="height: {tree_height}"></div>
    </div>
    {#if day_difference ===0}
      <h1>Merry Christmas!</h1>
    {/if}
    {#if day_difference !==0}
      <p>There are only</p>
      <p>{day_difference} days</p>
      <p>till Christmas {year}!</p>
    {/if}
  </section>
</main>

<style>
  main {
    width: 100vw;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #app-container {
    text-align: center;
  }

  #app-container p {
    margin: 0;
    font-size: clamp(2rem, 2vw, 3vw);
    line-height: clamp(3rem, 2.5vw, 3vw);
  }

  #mask-container {
    position: relative;
    width: 500px;
    height: 473px;
  }

  #mask-container img {
    position: relative;
    top: 0;
    -webkit-user-drag: none;
  }

  #colored-tree {
    position: absolute;
    top: 0;
    width: 500px;
    background-image: url('./assets/tree-color.png');
  }
</style>