<script lang='ts'>
  import { createEventDispatcher } from 'svelte';

  export let isOpen;

  const dispatch = createEventDispatcher();

  function handleClick(event: any) {
    dispatch('click', event);
  }
</script>

<style>
  .icon {
    width: 32px;
    height: 32px;
    fill: #000000;
    transition: fill 100ms ease;
  }

  .icon-button {
    width: 32px;
    height: 32px;
    background: none;
    border: none;
    padding: 0;
    margin: 0;
    cursor: pointer;
  }
</style>

<button class='icon-button' on:click={handleClick} aria-label='Menu'>
  {#if !isOpen}
    <svg class='icon' xmlns='http://www.w3.org/2000/svg' viewBox='0 -960 960 960'>
      <path d='M120-240v-66.67h720V-240H120Zm0-206.67v-66.66h720v66.66H120Zm0-206.66V-720h720v66.67H120Z'/>
    </svg>
  {:else}
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960">
      <path d="m256-200-56-56 224-224-224-224 56-56 224 224 224-224 56 56-224 224 224 224-56 56-224-224-224 224Z"/>
    </svg>
  {/if}
</button>

