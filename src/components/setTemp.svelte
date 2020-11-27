<script lang="ts">
  export let _id: string;
  export let set_temp: number;
  export let start_time: number;

  export let deleteTemp;

  var start_time_hours = new Date(start_time * 1000)
    .toISOString()
    .substr(11, 5);
</script>

<style>
</style>

<tr>
  <!-- TODO - actual col widths and style -->
  <td>{start_time_hours}</td>
  <td>{set_temp}</td>
  <td>
    <button type="button" on:click={() => deleteTemp(_id)}>Delete temp</button>
  </td>
</tr>
