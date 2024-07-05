<script>
  export let leftPadding = '0px';
  export let topPadding = '0px';

  $: customStyle = `padding-left: ${leftPadding};padding-top: ${topPadding};`;
</script>

<div style={customStyle}>
  <img src='/logo.svg' alt='Logo' />
</div>
