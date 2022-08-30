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

<h1>Rick and Morty Svelte</h1>

<div>
  <button on:click={previusPage} disabled={page === 1}> Previus </button>
  <button on:click={nextPage}> Next </button>
</div>

<div>
  {#each characters as character}
    <Character character={character} />
  {/each}
</div>
