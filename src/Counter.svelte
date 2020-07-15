<script>
	export let counter = 0;

	function handleClick () {
		counter ++;
  }
  
  $: numValidation = counter % 2 === 0 ? 'is even' : 'is odd';
</script>

<div>
	<button on:click={handleClick}>Incrementar</button>
	<p>{counter} = {numValidation}</p>
</div>

<style>

</style>