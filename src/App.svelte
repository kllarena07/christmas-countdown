<script lang="ts">
  const calculateDaysFromChristmas = () => {
    let today = new Date()
    let target_year = today.getMonth() + 1 === 12 && today.getDate() > 25 ? today.getFullYear() + 1 : today.getFullYear()
    let next_christmas = new Date(`12/25/${target_year}`)
    let difference = next_christmas.getTime() - today.getTime()
    return { difference: Math.ceil(difference / (1000 * 3600 * 24)), year: target_year }
  }

  let day_difference = calculateDaysFromChristmas().difference
  let year = calculateDaysFromChristmas().year
</script>

<main>
  <section id="app-container">
    <div id="mask-container">
      <img src="./public/tree-color.png" alt="holiday" />
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

  #app-container img {
    -webkit-user-drag: none;
  }
</style>