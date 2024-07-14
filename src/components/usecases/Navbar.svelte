<script>
  import '../../global.css';
  import Logo from '../modules/Logo.svelte';
  import SmallButton from '../modules/SmallButton.svelte';
  import NavigationLink from '../modules/NavigationLink.svelte';
  import MenuIcon from '../modules/MenuIcon.svelte';
  import BlackOverlay from '../modules/BlackOverlay.svelte';

  import { browser } from '$app/environment';
  import { onMount } from 'svelte';

  let lastScrollTop = 0;
  let isHidden = false;
  let isHamburguer = false;
  let isMenuOpen = false;

  function checkViewport() {
    isHamburguer = window.innerWidth < 644;

    if (!isHamburguer) {
      isMenuOpen = false;
    }
  }

  function handleScroll() {
    try {
      let scrollTop = 0; 

      if (browser) {
        scrollTop = window.scrollY;
      }

      if (scrollTop > lastScrollTop) {
        isHidden = true;
      } else {
        isHidden = false;
      }

      lastScrollTop = scrollTop <= 0 ? 0 : scrollTop;
    } catch (err) {
      console.error('Error accessing scroll position: ', err);
    }
  }

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  onMount(() => {
    window.addEventListener('scroll', handleScroll);
    window.addEventListener('resize', checkViewport);
    return () => {
      window.removeEventListener('scroll', handleScroll);
      window.removeEventListener('resize', checkViewport);
    }
  });
</script>

<style>
  nav {
    /* Positioning Properties */
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 1000;

    /* Layout Properties */
    display: flex;
    align-items: center;
    justify-content: space-between;

    /* Sizing Properties */
    height: 5.4em;
    padding: 0px 3.2rem;

    /* Color Properties */
    background-color: var(--background-color);
    border-bottom: 1px solid var(--contrast-color);
    box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.05);

    /* Animation Properties */ 
    transition: transform 0.3s ease, opacity 0.3s ease;
  }

  .hidden {
    transform: translateY(-100%);
    opacity: 0;
  }

  ul {
    display: flex;
    align-items: center;
    list-style: none;
  }

  .button-section {
    gap: 18px;
  }

  .main-nav-container {
    gap: 13px;
  }

  #nav-separator {
    font-weight: 700;
    font-size: 1.4rem;
    user-select: none;
  }

  .hamburguer {
    /* Positioning Properties */
    position: fixed;
    top: 0;
    left: 0;
    z-index: 998;
    transform: translateY(-100%);

    /* Sizing Properties */
    width: 100%;
    padding-top: 4rem;
    padding-bottom: 4rem;

    /* Color Properties */
    background-color: var(--background-color);

    /* Layout Properties */ 
    display: flex;
    align-items: center;
    justify-content: end;
    flex-direction: column;
    gap: 40px;

    /* Animation Properties */
    transition: transform 200ms ease;
  }

  .hamburguer.active {
    transform: translateY(5.4rem);
  }
</style>

<nav class:hidden={isHidden}>
  <Logo zindex="999" />

  {#if isHamburguer}
    <MenuIcon on:click={toggleMenu} isOpen={isMenuOpen} />
    <ul class={isMenuOpen ? 'hamburguer active' : 'hamburguer'}>
      <li><NavigationLink text='Home' url='#' /></li>
      <li><NavigationLink text='About' url='#' /></li>
      <li><NavigationLink text='Features' url='#' /></li>
      <li><NavigationLink text='Reviews' url='#' /></li>
      <li><NavigationLink text='Contact' url='#' /></li>
      <li><NavigationLink text='Sign in' url='#' /></li>
      <li><SmallButton title='Sign up' url='#' /></li>
    </ul>
  {:else}
    <ul class='main-nav-container'>
      <li>
        <ul class='button-section'>
          <li><NavigationLink text='Home' url='#' /></li>
          <li><NavigationLink text='About' url='#' /></li>
          <li><NavigationLink text='Features' url='#' /></li>
          <li><NavigationLink text='Reviews' url='#' /></li>
          <li><NavigationLink text='Contact' url='#' /></li>
        </ul>
      </li>
      <li>
        <span id='nav-separator'>|<span>
      </li>
      <li>
        <ul class='button-section'>
          <li><NavigationLink text='Sign in' url='#' /></li>
          <li><SmallButton title='Sign up' url='#' /></li>
        </ul>
      </li>
    </ul>
  {/if}
</nav>

<BlackOverlay on:click={toggleMenu} active={isMenuOpen} />
