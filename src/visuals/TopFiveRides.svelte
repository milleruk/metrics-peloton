<script>
  import ProgressBar from "../components/charts/ProgressBar.svelte";
  import {trimTitle} from "../utils/stringUtils";
  export let rides;
  export let color;
</script>

{#each rides as ride}
  <ProgressBar
    barLabel={ride.output}
    leftLabel={trimTitle(ride.title)}
    rightLabel={ride.instructor}
    fillColor={color}
    percentage={(ride.output / rides[0].output) * 100} />
{/each}
