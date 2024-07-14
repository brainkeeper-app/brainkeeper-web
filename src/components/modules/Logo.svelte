<script>
  export let url = "#";
  export let zindex = "0";

  $: customStyle = `z-index: ${zindex};`;
</script>

<a href={url} style={customStyle}>
  <img src='/logo.svg' alt='Logo' />
</a>
