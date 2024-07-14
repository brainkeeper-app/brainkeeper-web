<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  import { browser } from '$app/environment';

  export let active: boolean;

  const dispatch = createEventDispatcher<{
    click: MouseEvent;
  }>();

  function handleClick(event: MouseEvent) {
    dispatch('click', event);
  }

  function handleKey(event: KeyboardEvent) {
    if (event.key === 'Escape') {
      handleClick(event as unknown as MouseEvent);
    }
  }

  $: {
    if (active) {
      blockScroll();
    } else {
      unblockScroll();
    }
  }

  function blockScroll() {
    if (browser) {
      const scrollY = window.scrollY;
    
      document.documentElement.style.overflow = 'hidden';
      document.body.style.overflow = 'hidden';
      
      window.scrollTo(0, scrollY);
    }
  }

  function unblockScroll() {
    if (browser) {
      document.documentElement.style.overflow = '';
      document.body.style.overflow = '';
    }
  }
</script>

<style>
  div {
    display: block;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 998;
    opacity: 0;
    visibility: hidden;
    transition: opacity 200ms ease, visibility 0s linear 200ms;
  }

  .active {
    opacity: 1;
    visibility: visible;
    transition: opacity 200ms ease, visibility 0s linear;
  }
</style>

<div 
  on:click={handleClick} 
  on:keydown={handleKey}
  tabindex="0"
  role="button"
  aria-label="Black Overlay"
  class:active={active}
></div>
