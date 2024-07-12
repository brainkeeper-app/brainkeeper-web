<script>
  export let text = "Default Link";
  export let url = "#";
</script>

<style>
  a {

    /* Text Properties */
    text-decoration: none;
    font-size: var(--font-size-body);
    font-weight: 700;
    color: var(--text-color);

    /* Animation Properties */
    transition: color 100ms;

    user-select: none;
  }

  a:hover {
    color: var(--button-hover-color);
  }
</style>

<a href={url}>{text}</a>
