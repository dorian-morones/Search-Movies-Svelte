<script>
  let inputValue = '';

  const handleInput = (event) => inputValue = event.target.value;

  $: console.log(inputValue);
</script>

<input value={inputValue} on:input={handleInput} />