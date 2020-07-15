<script>
  let inputValue = '';
  let response = [];
  const handleInput = (event) => inputValue = event.target.value;

  $: if (inputValue.length > 2) {
    fetch(`https://www.omdbapi.com/?s=${inputValue}&apikey=422350ff`)
      .then(res => res.json())
      .then(apiResponse => {
        response = apiResponse.Search
      })
  }
</script>

<input value={inputValue} on:input={handleInput} />