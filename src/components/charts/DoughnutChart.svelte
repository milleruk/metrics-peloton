<script>
  import {onMount} from "svelte";
  import Chart from "chart.js/auto";
  import {convertStringToID} from "../../utils/stringUtils";

  export let title;
  export let datasets;
  export let chartReference = "";

  const ERROR_MESSAGE = "An error occurred creating the Output Chart";
  const chartID = "chart-" + convertStringToID(title);
  let isError = false;
  let screenWidth = 1200;

  const config = {
    type: "doughnut",
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: {
          position: "bottom",
        },
      },
    },
  };

  try {
    config.data = datasets;
  } catch (e) {
    isError = true;
    console.error(ERROR_MESSAGE, e);
  }

  onMount(async () => {
    try {
      const ctx = document.getElementById(chartID);
      chartReference = new Chart(ctx, config);
    } catch (e) {
      isError = true;
      console.error(ERROR_MESSAGE, e);
    }
  });
</script>

<style>
  div {
    position: relative;
    min-height: 50vh;
  }
</style>

<svelte:window bind:innerWidth={screenWidth}/>

{#if isError}
  <p>{ERROR_MESSAGE}</p>
{:else}
  <div class="chart-wrapper"><canvas id={chartID} /></div>
{/if}
