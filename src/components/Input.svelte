<script>
  export let required = false;
  export let placeholder = "";
  export let type = "text";
  export let name = "";
  export let value = "";
  export let onInput = "";
  export let id;
  export let label;
  export let className;

  $: if (!value) value = "";

  import { namesData as data } from "../data.js";
</script>

<label for={id}>{label}</label>
{#if type === 'select'}
  <select {required} {name} {className} {id} bind:value on:input={onInput}>
    <option selected>Search for Your Name</option>
    {#each data as name}
      <option>{name.firstname} {name.lastname}</option>
    {/each}
  </select>
{:else if type === 'text'}
  <input {required} {name} {id} {className} bind:value on:input={onInput} />
{/if}
