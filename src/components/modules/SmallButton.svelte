<script>
  export let title = 'Default Title';
  export let url = '#';
</script>

<style>
  a {
    /* Text Properties */
    text-decoration: none;
    font-size: var(--font-size-body); 
    font-weight: 700;
    color: #f8f8ff;
    
    user-select: none;

    /* Layout Properties */
    display: inline-flex;
    align-items: center;

    /* Sizing Properties */
    height: 34px;
    padding: 0px 15px;
    border-radius: 12px;

    /* Color Properties */
    background-color: var(--primary-color);

    /* Animation Properties */
    transition: background-color 100ms;
  }
  
  a:hover {
    /* Color Properties */
    background-color: var(--button-hover-color);
  }
</style>

<div>
  <a href={url}>{title}</a>
</div>
