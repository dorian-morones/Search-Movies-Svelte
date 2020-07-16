<script>
  import Movie from './Movie.svelte';

  let value = ''
  let loading = false
  let response = []

  const handleInput = (event) =>
    value = event.target.value

  $: if (value.length > 2) {
    loading = true
    fetch(`https://www.omdbapi.com/?s=${value}&apikey=422350ff`)
      .then(res => res.json())
      .then(apiResponse => {
        response = apiResponse.Search || []
        loading = false
      })
  }
</script>

<style>
  .inputContainer{
    display: flex;
    justify-content: center;
    width: 100%;
    padding: 10px;
    background-color: #fff;
    box-shadow: 0 -0.4rem 0.9rem 0.2rem rgba(0,0,0,.5);
  }
  .moviesContainer{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 20px;
    padding: 20px;
  }

  input{
    border: none;
    border-bottom: solid 1px #ff3e00;
    border-radius: 0px;
    width: 300px;
  }
</style>

<div class="inputContainer">
  <input
    placeholder="Search movies..."
    value={value}
    on:input={handleInput}
  />
</div>

{#if loading}
  <strong>Loading...</strong>
{:else}
  <div class="moviesContainer">
    {#each response as {Title, Poster, Year}, index}
      <Movie
        index={index}
        title={Title}
        poster={Poster}
        year={Year}
      />
    {:else}
      <strong>No hay resultados</strong>
    {/each}
  </div>
{/if}
