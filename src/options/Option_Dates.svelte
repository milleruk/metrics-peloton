<script>
  import {dateFilter} from "../store/store.js";

  let startDate = $dateFilter.startDate;
  let endDate = $dateFilter.endDate;

  const updateDateFilters = () => {
    dateFilter.set({startDate, endDate});
  };
</script>

<style>
  .option-wrapper{
    margin-bottom: 20px;
  }
  .option-label {
    display: block;
    margin-bottom: 10px;
  }
  button, input{
    display:block;
  }
  .label-container{
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    justify-content: space-evenly;
  }
  .label-container{
    flex: 0 1 50%;
    min-width: 150px;
  }
</style>

<div class="option-wrapper">
  <h3>Filter By Date</h3>
  <p>Start Date defaults to 9 months from the latest ride.</p>
  <p>Note: If you go too far back, the amount of rides may render the chart unreadable.</p>
  <form on:submit|preventDefault={updateDateFilters}>
    <div class="label-container">
      <label class="option-label">
        Start Date  <input
          type="date"
          bind:value={startDate}
          placeholder="yyyy-mm-dd"
          class="option-field" />
      </label>
      <label class="option-label">
        End Date  <input
          type="date"
          bind:value={endDate}
          placeholder="yyyy-mm-dd"
          class="option-field" />
      </label>
    </div>
  <button class="normal-button" type="submit">Set</button>
  </form>
</div>