<script>
  import Week from './Week.svelte';

  export let id;
  export let visibleMonth;
  export let selected;
  export let highlighted;
  export let shouldShakeDate;
  export let daysHighlighted;

  let lastId = id;
  let direction;
  let listDaysHighlighted = [];

  $: {
    direction = lastId < id ? 1 : -1;
    lastId = id;
    listDaysHighlighted = daysHighlighted;
  }
</script>

<div class="month-container">
  {#each visibleMonth.weeks as week (week.id) }
    <Week 
      days={week.days} 
      {selected} 
      {highlighted} 
      {shouldShakeDate}
      daysHighlighted={listDaysHighlighted}
      {direction}
      on:dateSelected 
    />
  {/each}
</div>

<style>
  .month-container { 
    width: 100%;
    display: -ms-grid;
    display: grid;
    -ms-grid-columns: 1fr;
    -ms-grid-rows: 1fr;
  }
</style>
