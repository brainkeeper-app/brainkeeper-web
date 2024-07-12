<script>
  import '../../global.css';
  import Logo from '../modules/Logo.svelte';
  import SmallButton from '../modules/SmallButton.svelte';
  import NavigationLink from '../modules/NavigationLink.svelte';

  import { browser } from '$app/environment';
  import { onMount } from 'svelte';

  let lastScrollTop = 0;
  let isHidden = false;

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

  onMount(() => {
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
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
    padding: 0px 32px;

    /* Color Properties */
    background-color: var(--background-color);

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
</style>

<nav class:hidden={isHidden}>
  <Logo />
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
</nav>

