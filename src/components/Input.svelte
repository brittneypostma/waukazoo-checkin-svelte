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
  import { onMount } from "svelte";
  $: if (!value) value = "";

  import { namesData as data } from "../data.js";
  onMount(() => {
    const input = document.getElementById("volunteersList");
    input.addEventListener("click", handleToggleSearch);
  });

  const toggleClick = () => {
    let liValue = document.getElementsByTagName("li").value;
    let inputValue = document.getElementById("volunteersList").value;
    inputValue = liValue;
    console.log(inputValue, liValue);
  };
  let clickedSearch = false;

  const handleToggleSearch = () => {
    clickedSearch = !clickedSearch;
  };

  function filterFunction() {
    let input = document.getElementById("volunteersList");
    const filter = input.value.toUpperCase();
    let li = document.getElementsByTagName("li");

    for (let i = 0; i < li.length; i++) {
      let txtValue = li[i].textContent || li[i].innerText;

      if (txtValue.toUpperCase().indexOf(filter) > -1) {
        li[i].style.display = "";
        value = li[i].value;
      } else {
        li[i].style.display = "none";
      }
    }
  }
</script>

<style>
  input {
    outline-color: #e74c3c;
    width: 100%;
  }

  #volunteersList {
    width: 100%;
    padding: 12px 20px;
    border: 1px solid #ddd;
    margin-bottom: 0;
  }

  .displayList {
    max-height: 200px;
    overflow-y: scroll;
    overflow-x: hidden;
    position: relative;
    top: -5%;
  }

  #myUL {
    list-style-type: none;
    padding: 0;
    margin: 0;
  }

  li {
    border: 1px solid #ddd;
    margin-top: -1px; /* Prevent double borders */
    background-color: #ffffff;
    padding: 2px;
    text-decoration: none;
    font-size: 16px;
    color: black;
    display: block;
  }
  li:nth-child(odd) {
    background-color: #ddd;
  }

  li:nth-child(even) {
    background-color: #eee;
  }

  li {
    background-color: rgb(255, 255, 255);
    transition: all 0.2s ease;
  }

  li:hover {
    background-color: #333;
    color: white;
    cursor: pointer;
  }
</style>

<label for={id}>{label}</label>
{#if id === 'volunteersList'}
  <input
    {required}
    {name}
    {className}
    {placeholder}
    id="volunteersList"
    bind:value
    on:input={onInput}
    on:keyup={filterFunction} />
  {#if clickedSearch}
    <div class="displayList">
      <ul id="myUL">
        {#each data as name}
          <li class="list">{name.firstname} {name.lastname}</li>
        {/each}
      </ul>
    </div>
  {/if}
{:else if type === 'text'}
  <input {required} {name} {id} {className} bind:value on:input={onInput} />
{/if}
