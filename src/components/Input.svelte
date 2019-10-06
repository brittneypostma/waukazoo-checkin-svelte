<script>
  export let required = false;
  export let placeholder = "";
  export let type = "";
  export let name = "";
  export let value = "";
  export let onInput = "";
  export let selected;
  export let id;
  export let label;
  export let className;

  $: if (!value) value = "";

  import { namesData as data } from "../data.js";
</script>

<div>
  <label for={id}>{label}</label>
  {#if type === 'select'}
    <select {required} {name} {id} bind:value on:input={onInput}>
      <option selected>Search for Your Name</option>
      {#each data as name}
        <option>{name.firstname} {name.lastname}</option>
      {/each}
    </select>
  {/if}

  {#if type === 'text'}
    <input {required} {name} {id} {className} bind:value on:input={onInput} />
  {/if}

</div>
