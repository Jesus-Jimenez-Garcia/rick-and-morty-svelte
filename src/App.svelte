<script>
  import Character from "./lib/Character.svelte";

  let characters = [];
  let page = 1;

  async function loadCharacters() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    characters = data.results;
    console.log(characters);
  }
  loadCharacters();

  function nextPage() {
    page++;
    loadCharacters();
  }

  function previusPage() {
    page--;
    loadCharacters();
  }
</script>

<h1 class="title">Rick and Morty Svelte</h1>



<div class="container">
  <div class="btns">
    <button on:click={previusPage} disabled={page === 1} class="btn"> Previus </button>
    <button on:click={nextPage} class="btn"> Next </button>
  </div>
  <div class="grid">
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>
</div>
